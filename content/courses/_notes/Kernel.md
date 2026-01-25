Multi-threaded Kernel: OS kernel designed to support multiple threads within a single process.
- System library allocates a user-space stack for each user-level thread.
	- Uses system calls to create, join, yield, exit threads
- Kernel handles scheduling and context-switching using kernel-space stacks

To create a thread:
```cpp
// dummy function to start the thread
stub(void *(*func)(void*), void *args) {
	// execute the function func()
	(*func)(arg);
	// if func() does not call exit, call it here
	thread_exit(0);
}

thread_create(void *(*func)(void*), void *args) {
	// Allocate TCB
	TCB *tcb = new TCB()
	// Allocate kernel stack
	tcb->stack = new Stack(INITIAL_STACK_SIZE)
	// Initialize SP & PC
	tcb->sp = tcb->stack + INITIAL_STACK_SIZE;
	tcb->pc = stub;
	// set up kernel stack: push function and args
	*(--tcb->sp) = args;
	*(--tcb->sp) = func;
	// set up entry point
	*(--tcb->sp) =  stub;
	// push dummy data for handler_exit
	push_dummy_handler_frame(&tcb->sp);
	// set up return address for thread_switch
	*(--tcb->sp) = Handler_Exit;
	// push dummy data for thread_switch
	push_dummy_switch_frame(&tcb->sp);
	// set state of thread to ready
	tcb->state = READY;
	// put TCB on ready list
	readyList.add(tcb);
}
```
Some caveats about this code block:
- Why not just set tcb->pc to func?
	- This extra step is required in case "func" procedure returns instead of calling `thread_exit`.
	- If it simply returns, func would return to whatever random location is stored at top of stack.
- Stack starts at top of allocated region and grows down. 
	- Essentially, it goes from address stored in tcb->sp down to tcb->stack.

What triggers a context switch?
Context switch -> suspends execution of currently running thread and resumes execution of some other thread
1. Voluntary: thread calls a thread library function or system calls
   e.g. yield, join, exit, open, write, read
2. Involuntary: interrupts or exceptions invoke a handler
   Can decide to switch or continue when handler is done
   e.g. timer interrupt, new packet arrives, DMA request finishes

Consider this example of a voluntary context switch i.e. yielding a thread

Assume `thread_yield()` makes a system call that transfers to kernel mode through `kernel_yield()`. 
```c
void compute_PI() {
	while(TRUE) {
		compute_next_digit();
		thread_yield();
	}
}
```

```c
// we enter as oldTCB, but return as newTCB
// return with newTCB's registers and stack
thread_switch(TCB *oldTCB, TCB *newTCB) {
	// push all regs onto kernel stack of oldTCB
	// set oldTCB->sp to stack pointer
	// set stack pointer to newTCB->sp
	// pop regs from kernel stack of newTCB
	// return
}

void kernel_yield() {
	// temporarily disable interrupt
	disable_interrupts();
	// choose another tcb from ready list
	chosenTCB = scheduler.getNextTCB();
	if (chosenTCB != runningTCB) {
		// move running thread onto ready list
		runningTCB->state = READY;
		// move running thread onto ready list
		runningTCB->state = READY;
		ready_list.add(runningTCB);
		// switch to the new thread
		thread_switch(runningTCB, chosenTCB);
		// run!
		runningTCB->state = RUNNING;
		// cleanup?
		do_cleanup_housekeeping();
	}
	enable_interrupts();
}
```
There are few things to note here:
- Why disable interrupts? To prevent thread system from making two context switches at the same time
- When we set it to RUNNING, we come back to where we had left off before hand
- If the thread has never run before (i.e. newly created), this will pop the function and arguments. To fix this, we push a `dummy_switch_frame` when creating a thread and set SP initialized to stub.

In regards to entry point of threads,
- kernel threads don't require a mode switch
- user threads switch from kernel to user mode as we need one level of "indirection"
	- alternative: jump to a kernel code that then jumps to user code and changes mode atomically
More explanation:
- kernel threads are in kernel space so no need for a mode switch
- user threads need to switch from kernel to user mode to access resources/code in user space (i.e. indirection)
	- the kernel code is a small piece that allows this transfer to happen. (kernel --> kernel (mode-switch)    --> user)
	- this happens either during return from interrupt handler or system call.

```c
handler() {
	// this runs in kernel mode
	// SP points to a kernel stack

	// push regs used by handler on kernel stack
	// i.e. save user mode

	// handle event
	
	Handler_Exit:
	// pop regs that were pushed - i.e. restore state
	// return - change kernel to user mode
}
```

Understanding **kernel-managed and user-managed threads**
- Kernel-managed threads i.e. thread ops implemented in kernel
	- OS schedules the threads in system and each user thread maps to one TCB (can run or block independently)
	- expensive! crossing into kernel mode to schedule and more expensive than procedure call
- User-managed threads i.e. threads managed by user-level library (pthreads)
	- user process creates threads and schedules it
	- kernel is not aware of multiple threads
	- allocates single TCB to user process, i.e. cheaper with no kernel involvement
	- drawbacks
		- single core limitation - can't take advantage of multi-core processors since kernel schedules processes
		- no pre-emptive scheduling - one thread can starve other threads with no kernel to pre-empt this
		- blocking calls - one blocking call will block all threads/process
	- The alternative is: scheduler activations
		- notify user-level scheduler of relevant kernel events essentially (through upcalls)
			- request more CPU time; threads blocked on I/O or timer interrupts etc.

Classification of OS can look like

| #addr_space ><br><br>#threads v | One           | Many                   |
| ------------------------------- | ------------- | ---------------------- |
| **One**                         | MS/DOS        | Traditional UNIX       |
| **Many**                        | Embedded Sys. | Linux, Windows 10, OSX |
