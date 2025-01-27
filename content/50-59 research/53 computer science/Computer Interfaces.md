---
title: Computer Interfaces
---
**Sensors** - device that sense or detect physical properties of a system
- reacting to a measured condition of the system by creating an output electrical signal
- so, a light sensor is looking for some lumen value and when it detects it, it outputs a signal
**Actuators** - devices that move or control the operation of a system
- respond to an input signal by controlling an operation
- so, a fuse would break connection when seeing a surge in electricity

**I/O interfaces**
- purpose: convert external signals to appropriate levels + timing with system

**What are the sig. design issues to consider when designing I/O interfaces?**
- Signalling Issues
	- how is data represented? *Analog or digital signal*
	- sources of misinterpretation *noise, timing, signal levels*
- Dataflow Issues
	- what info is being transferred? *event, data, data+event*
	- direction of data transfer? *unidirectional, bidirectional*
	- follow up, device that controls flow of data
	- validity of data
- [[Synchronization]] Issues
	- level of service? *active or passive syncing i.e. interrupt vs polling*
	- how to achieve syncing? *methods to be discussed later anyways*
	- when is data generated? *event-generated, spontaneous*
