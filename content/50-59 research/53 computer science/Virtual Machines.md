Virtual Machine: Created by a hypervisor which abstracts hardware of a single computer into different execution environments e.g. [[100 Study/104 Subject-Specific Learning/104.2 Programming/Operating System|OS]]

The benefits of VMs:
- application portability
	- support legacy programs that run on old OS versions; 
	- enable rapid porting of programs in different environments
- OS research and development
	- isolate development and bugs from host machine
	- allow for debugging
	- system-development time i.e. system is stopped and taken out of use to make changes

> [!note] Virtualization vs. Emulation
> Virtualization is running applications compiled for an OS on a different OS
> - execution environment: virtual machine
> - relatively efficient since host and guest machine use same ISA
> 
> Emulation is running applications compiled for one architecture on a different architecture
> - execution environment: emulator
> - slower because translation between different ISA's is needed

