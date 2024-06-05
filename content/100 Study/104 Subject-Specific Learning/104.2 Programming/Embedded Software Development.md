---
title: Embedded Software Development
---
**Embedded System** - this is a special purpose computer system designed to perform tasks without the user even realizing it exists
- user might provide input to the system through sensors/actuators but doesn't mean we know it exists

**View of Embedded Systems**
- View A: System-centric view where we consider interaction between emb. sys. and environment
	- Focus is on the system to control, in open or closed loop
- View B: Computer-centric view where computer implements instr. in software to control system i.e. it's more about letting embedded system to make it's own decisions as opposed to a response to some external stimuli

**Cross Platform Development**
process in which software is designed, compiled and tested for a target computer system using a host computer
- embedded systems can not "compile" code so must be done externally

**hardware/software codesign** - task of simultaneously designing the hardware and software components of a system
- **computer hardware** - mechanical/electrical components of a computer
- **computer software** - programs or other operating info. used by a computer

embedded control programs - a single program that will control the entire system with the following app flow
- initialize + enable all devices to be used
- in infinite loop
	- check status of input devices
	- how to respond to input devices
	- update output devices
- program only ever terminates upon shut down

How to communicate with I/O devices?
- main program directly accesses registers of I/O devices using memory-mapped I/O
- more advanced: functions provided by a board-support package (labs)
- if it runs a full OS, communicate using device drivers

**Input and Output Interfaces**
- I/O interfaces connect the computer to outside world, requires conversion of external signals to appropriate levels and appropriate timing for interaction with the system
- Some of the significant design issues are:
	- Signalling issues
		- Data is represented by electronic signals in two forms: Digital and Analog
		- A signal can be "misinterpreted" due to
			- noise (permanent/transient) where 
				- Permanent Error: Able to reproduce in repeatable experiments,
				- Transient Error: Sometimes reproducible in repeatable experiments,
			- timing (high-speed data transmission, transient data, sampling error),
			- signal levels (current range, voltage range, ground reference)
				- In analog (AC) signals, where it's continuous and the difference between two voltages is low, this is frequent issue
	- Dataflow issues
		- What is the information transferred? (not sure what the issue here is)
		- Direction of data transfer can be unidirectional (data flow in single direction), or bidirectional (data flow in both directions)
			- How can we control when it's in input/output
		- Which device controls the flow of data? 
			- Imagine connection between two computers - who talks first?
		- How is the presence of valid data indicated?
	- [[Synchronization]] issues
		- Are the communicating entities equals? Case with two computers communicating
		- What level of services is required?
			- Active sync is demand-oriented e.g. interrupts need immediate service
			- Passive sync is request-oriented e.g. poll to detect need for service
		- How will syncing be achieved?
			- Interrupts, Polling loops and Blind syncing
		- When will data be generated? Generate spontaneously or in response to an event

**levels of abstraction** - how a main program actually accesses I/O devices, not in modern OS (see drivers)

**device drivers:** privileged extension of the kernel of an OS to support communication with a particular I/O device
- sync I/O should be avoided to prevent bottlenecks
	- why? it will block execution of program until something is done happening.

**microprocessor** - consists of a processor only (no main memory and no built-in support for I/O devices)
**microcontroller** - complete computer on a single chip with processor, memory and some I/O devices