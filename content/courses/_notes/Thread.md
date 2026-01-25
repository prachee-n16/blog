*Thread of execution;* sequence of executable commands that run on CPU

Threads, like [[Process|process]], have an 
- execution state in the lifecycle
- saved context when not running 
- execution stack
	- this is maintained in their thread control block i.e. data structure in OS containing information needed to manage a thread

When saving memory for threads:
- We choose a max size for thread stacks and if threads violate this, terminate program or corrupted data
	- these violations can be caught by placing guard values at top and bottom of each stack

Some discussions on performance: 
1. Threads are good for:
	1. Program Structure: expressing logically concurrent tasks
	2. Responsiveness: Shift work to run in background (daemon)
	3. Performance: Exploits parallelism in hardware i.e. spread out tasks in different computing units to improve latency and throughput
2. If we compare multiple processes vs. single process with multiple threads
	- the fundamental trade-off is between protection and efficiency
	- it is harder to communicate between processes and requires IPC
	- it is easier to communicate within a process, but less secure

For OS, we make a distinction between kernel thread and user thread.

For kernel threads,
- all thread operations are implemented in kernel
### Implementation of Threads
This section covers a general implementation of threads in C, for multi-threaded kernels.
###### Create a thread
```cpp
thread_create(void *(*func)(void*), *args) {
	TCB *tcb = new TCB();
	// allocate stack for kernel
	tcb->stack = new Stack(INITIAL_STACK_SIZE);
	tcb->sp = tcb->stack + INITIAL_STACK_SIZE;
	tcb->pc = stub;
	// set up arguments and function in stack pointer
	*(--tcb->sp) = args;
	*(--tcb->sp) = func;
	// sets up entry point to thread
	*(--tcb->sp) = stub;
	// we push this because in yield, we pop regs from kernel stack
	push_dummy_switch_frame(&tcb->sp);
	// set the state of task
	tcb-->state = READY;
	readyList.add(tcb);
}

// We initialize to this stub function if the func() does not call exit
stub(void *(*func)(void*), void *args) {
	(*func)(arg);
	thread_exit(0);
}
```
###### Yield a thread
```cpp
void kernel_yield() {
	disable_interrupts();
	chosenTCB = scheduler.getNewTCB();
	if (chosenTCB != runningTCB) {
		runningTCB.state = READY;
		readyList.add(runningTCB);
		thread_switch(runningTCB, chosenTCB);
		chosenTCB.state = RUNNING;
		do_cleanup_housekeeping()
	}
	enable_interrupts();
}

thread_switch(TCB *oldTCB, TCB *newTCB) {
	Push all regs from kernel stack to oldTCB
	Set oldTCB->sp to stack pointer
	Set stack pointer to newTCB->sp
	Pop all regs from kernel stack of newTCB
	Return
}
```

The context switch is triggered:
1. Voluntary: thread calls a thread library function or system call
2. Involuntary: interrupts or exceptions invoke a handler
	- can decide to switch or continue when handler is done
