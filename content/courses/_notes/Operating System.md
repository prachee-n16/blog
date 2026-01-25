*Special layer of software that provides application access to hardware resources*

> [!note] Table of Contents
> - Roles of the OS
> - Hardware Support with OS
> - Virtualization and [[Virtual Machines]]
> - [[Real-time Systems]]
> - Trends in OS Development

**Roles of Operating System**
- Illusionist
	- provides clean, easy to use abstractions of physical resources
		1. Simplified Interface 
			- Think about how [[File System|file systems]] simplify storage or virtual memory simplify [[DRAM]]  
		2. Mask hardware limitations
			- Provide the illusion of *dedicated processor and infinite memory*, while really working with a *time-shared processor and limited memory*
- Referee
	- help with context switching in safe and secure manner
	- provide protection, isolation and sharing of resources
		1. Resource Allocation: Share physical memory, network bandwidth and disk space
		2. Isolation: A process can't read another processes' or OS' memory
		3. Communication: explicitly request shared memory
- Glue
	- provide common services
		- standardized file system, window system or device drivers
	- benefits:
		- let apps focus on their core tasks, and let users have same look and feel as they switch between apps
		- background management of tasks like power/battery

**Hardware Support**
- OS has low performance overhead over raw hardware
- It uses hardware support to provide these abstractions efficiently
	- dual-mode operation => control register
	- I/O management => interrupt
	- process management => timer
	- address translation => TLB; translation lookaside buffer

**Trends in OS Development**
- moore's law: number of transistors on a microchip doubles approximately every two years
	- **Power density**: Moore's Law extrapolation shows potential power densities reaching extremely high levels, posing significant cooling and power delivery challenges.
- dennard scaling: as transistors get smaller, their power density stays constant, allowing higher performance without increasing power consumption
	- With the end of Dennard scaling, **parallelism** (using multiple cores and threads) is essential to improve performance.
- dark silicon: as chips get more cores, only a fraction can be powered on simultaneously due to power constraints
- accelerator era: specialized accelerators for specific tasks to continue performance improvements
- The growth rate of single-thread performance has slowed down due to physical and technological limitations.
	- Emphasizes using multiple processor cores to increase performance since single-core performance improvements are limited.

In short:
- Transistors: Continued exponential growth.
- Frequency (MHz): Stagnation after hitting power limits.
- Number of Cores: Increased as a response to the end of Dennard scaling.

**The fundamental OS concepts:**
- [[Thread]]
- [[Process]]
- [[Address Space]]

> [!note] Parallelism in Modern CPU Architectures
> 1. Superscalar (wide pipeline)
>    - Executes multiple instructions per cycle within a single core
>    - exploits instruction-level parallelism  
>
> 2. Multicore
>    - Multiple cores executing independent threads; focuses on thread-level parallelism
>    - exploits thread-level parallelism  
>    
> 3. Fine-grained Multithreading; FGMT
>    - Single core executes multiple threads by switching between them each cycle
>    - exploits thread-level parallelism  
>    
> 4. Simultaneous Multithreading; SMT
>    - Single core executes multiple threads simultaneously;
>    - exploits thread-level parallelism  

Putting it together,
1. Process
   - switch overhead is high
	   - CPU state e.g. PC, SP, General Purpose Registers
	   - Memory/IO state 
   - process creation is high
	   - why? setting up page tables is an expensive operation
   - protection
	   - CPU: yes
	   - Memory/IO: yes
   - sharing overhead: high
	   - involves at least one context switch; also, requires IPC
2. Threads
	- switch overhead is medium
		- CPU state is low
		- Memory/IO state is zero for threads with a process
	- thread creation is low
	- protection
		- CPU: yes
		- Memory/IO: no
	- sharing overhead: low
		- memory shared among threads
3. Multi-cores
	- switch overhead is low
		- assume map all threads from same process to same core
	- thread creation is low
	- protection
		- CPU: yes
		- Memory/IO: no
	- sharing overhead: low
4. SMT (simultaneous multithreading)
	- switch overhead between hardware threads: very-low
		- done in hardware: register files tagged with thread ID
	- contention for shared resources may hurt performance

