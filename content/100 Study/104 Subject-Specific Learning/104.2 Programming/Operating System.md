*Special layer of software that provides user applications access to hardware resources*

Ideally, it has low performance overhead over raw hardware. 
- Dual-mode operation --> Control Register
- I/O management --> Interrupts
- Process Management --> Timer
- Address Translation --> Translation Lookaside Buffer

In general, it has 3 roles: [[#Illusionist]], [[#Glue]], [[#Referee]]. 
###### Illusionist
- Provide a simple interface for users to work with
	- e.g. File Systems simplify storage by allowing named files, file organization etc.
	- e.g. Virtual Memory simplifies how a process owns memory within [[100 Study/104 Subject-Specific Learning/104.2 Programming/DRAM]] 
- Mask hardware limitations
	- Each process feels like it has a dedicated processor with nearly infinite memory; contrary to reality
###### Glue
- Provides common services such as standardized file systems, device drivers etc.
- Allows applications to focus on their tasks 
###### Referee
- Provides protection, isolation and sharing of resources
	- Allocate resources such as physical memory, network bandwidth, disk space for processes
	- Ensure a process can't read other process/OS's memory
		- In fact, a process needs to explicitly request for shared memory
- Allows for context-switching between different process