divides the execution environment into two distinct modes: user mode and kernel mode
- virtual memory provides process isolation but does not prevent direct tamper with hardware

User mode: applications are designed to run with restrictions
- processor executes a subset of instruction set
- privileged instructions = instructions available in kernel mode
Kernel mode: supervisor/protected mode; special mode of the processor for executing trusted code without any restrictions

We can think about these restrictions as "privilege rings": different levels of access to resources
![500](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Priv_rings.svg/1200px-Priv_rings.svg.png)
- Ring 0: Kernel mode 
	- access to all privileged instructions and mapped virtual memory
- Ring 1 + 2: Device drivers
	- no access to privileged instructions but some I/O commands; access to all mapped virtual memory
- Ring 3: user mode
	- only non-privileged instructions; only user-accessible virtual memory
The current privilege level is stored in some processor **control register**
- x86: lower 2 bits of the Code Segment (CS) registe
- Arm: lower 4 bits of the Current Program Status Register (CPSR)
Bits are set/cleared during mode transfer

**Types of Mode Transfer**
- User to Kernel
	- system call: request for kernel services; implemented by calling syscall instructions or traps
	- processor exception: internal, synchronous, hardware event which is caused by software behavior
	- interrupt: external asynchronous event
- Kernel to User
	- new process/thread start: jump to first instruction
	- return from interrupt/execution/system call
	- process/thread context switch
	- user-level upcall i.e. asynchronous notification to user program
- For a safe mode transfer:
	- limited entry into kernel: hardware must ensure entry point into kernel in set up by kernel itself
	- atomic transfer of control
		- single instruction to change PC/SP/mode bit
	- transparent, resumable execution where user program can't tell interrupt occurred
- The processor uses interrupt vector tables to understand which interrupt handler to load
	- In x86, it's a table of 256 entries where index = interrupt# and entry = handler address 
- allocate separate kernel interrupt stacks for each user-level thread
	- why? processor will overwrite PC with kernel handler address
		- so, we need to save the PC and registers
		- therefore, kernel handler execution needs a stack
	- We can not save anything in the user stack because:
		- all threads in the process have access to it
		- user might not write bug-free multi-threaded programs 
	- OS's might go another step further and allocate separate stacks for every user-level thread
		- makes it easier to context switching inside an interrupt/system call handler

The steps for this mode transfer:
- Mask interrupts
- Save PC, SP and execution flags in temporary HW registers  
- Switch onto kernel interrupt stack (specified in special HW registers)  
- Push the three key values onto interrupt stack  
- Optionally save an error code  
- Invoke interrupt handler

why are we doing [[Interrupts|interrupt]] masking here?
- Interrupt handler runs with interrupts disabled.
	- Simplifies the process of handling interrupts
- Disabled interrupts are deferred (masked), not ignored.
- Interrupts are re-enabled when the interrupt handler completes.
