**Definitions**
1. Task: Also called thread, process, job is a unit of work
2. Workload: Set of tasks
3. Scheduling algorithm: Takes the workload as input and decided which tasks to do first
4. Overhead: Extra work done by scheduler that is not a task
5. Preemptive scheduler: CPU can be taken away from a running task
6. Work-conserving scheduler: CPU's won't be left idle if there are ready tasks to run


**Overview**
- Process execution consists of a cycle of CPU bursts and I/O bursts. 
- CPU Scheduling: choosing which thread gets CPU for next CPU burst. 
	- These decisions take place when a process:
		- switches from running to waiting (nonpreemptive)
		- switches from running to ready (preemptive)
		- switches from waiting to ready (preemptive)
		- terminates (nonpreemptive)
- Goal: Improve CPU utilization through multitasking. 
- We consider performance metrics for CPU
	- Minimize average response time != latency
		- latency is the time from start to finish
		- response time is the time from "arrival to finish" i.e. for a user
	- Maximize throughput i.e. tasks completed per time unit
		- This can be divided into sub-goals of:
			- minimize overhead e.g. context-switching
			- efficient use of resources
- We consider fairness metrics for CPU
	- Share CPU time among users in some equitable way

**CPU Scheduling Algorithms**
- [[FCFS Scheduling]]