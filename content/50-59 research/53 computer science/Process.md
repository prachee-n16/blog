A process is a running instance of a program (i.e. static bytes sitting on a disk)
- OS's abstraction of execution which contains
	- virtual address space
	- CPU states: PC, SP, General-purpose registers
	- OS resources (can be files, network connections etc.)

From program to process, 
- Load instruction/data of executable file i.e. program into memory
- Set up the initial stack and other initialization tasks
	- construct new PCB; *cost: inexpensive*
	- set up new page tables for [[Address Space|address space]]; *cost: more expensive*
	- copy data from parent process; *cost: less expensive with copy on write*
	- copy I/O state; *cost: medium expensive*
- Transfer control to program
Generally, the process then maintains the following lifecycle: [Process Lifecycle](https://www.geeksforgeeks.org/states-of-a-process-in-operating-systems/)
![[thread_lifecycle.png]]

To help with process management:
1. Process Control Block (PCB)
	- data structure created by OS to manage processes
		- contains everything OS needs to know and OS keeps it up to date
	- it is kept in memory and maintained in some container by kernel
2. State Queues
	- collection of queues maintained by OS to represent state of all processes in system

> [!note] Mechanism and Policy
> Mechanisms: low-level methods or protocols that implement a needed piece of functionality
> - context switch: mechanism of switching CPU from running one process to another 
> 	- triggered by timer, voluntary yield, interrupts
> 	- this switch from one process to another requires us to :
> 		- save PC, SP, and registers to current PCB
> 		- load PC, SP, and registers from new PCB
> 
> Policies: algorithms for making some kind of decision
> - round robin scheduling: policy of switching between multiple processes that ensures fairness

