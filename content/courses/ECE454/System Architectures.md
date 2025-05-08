[[Distributed System|Distributed Systems]] and Parallel systems can be organized in many ways.

> [!note] Models for Parallel System 
> There are a **four key models** of parallel computing architectures:
> 1. SIMD (Single Instruction Multiple Data) uses same instruction on multiple data points which makes it good for vector ops and data-parallel tasks
> 2. SMT (Simultaneous Multithreading) where multiple threads issue instructions to a single  core, seen in GPU and CUDA models
> 3. MIMD (Multiple Instruction Multiple Data) where a processor executes executes different instructions on different data 
> 4. SPMD (Single Program Multiple Data) where all processors execute the same program but on different data

For distributed systems, we consider **models** and **styles** alike.

## Distributed Architecture Model

*Client-Server Architecture*
![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Client-server-model.svg/1200px-Client-server-model.svg.png)


*Master-Worker Architecture*
![200](https://miro.medium.com/v2/resize:fit:850/1*fx1xvD2LF7bwc5qSaRn4yw.png)

*Peer-to-Peer / Compute Cluster*
![200](https://upload.wikimedia.org/wikipedia/commons/9/9e/P2P_network.svg)

## Distributed Architecture Styles

*Layered Architecture* 
- Layered architecture separates system components into distinct logical layers, promoting modularity and clear responsibilities.
- Flow of Control:
	- Requests flow downward from higher layers to lower layers.
	- Responses flow upward from lower layers back to the origin.
- Example: OSI Model is a classic implementation, with 7 layers handling network communication.
![](https://miro.medium.com/v2/resize:fit:720/format:webp/0*9tldQrHipUK3DjbB.png)


*Object-based Architecture*
- Based on loosely coupled objects that communicate via well-defined interfaces, without following a strict sequence of steps like in layered systems.
- Flow of Control:
	- Objects interact directly via method calls, often across network boundaries.
![](https://miro.medium.com/v2/resize:fit:720/format:webp/0*At9J87uG-JJmrU1J.png)

*Data-centered Architecture*
- Revolves around a central data repository that serves as the main medium for communication between components.
- Flow of Control:
	- Follows a producer-consumer pattern:
		- Producers write data to the shared storage.
		- Consumers read data from the same source.
	- Components do not communicate directly with each other but through the data hub.
![](https://miro.medium.com/v2/resize:fit:720/format:webp/0*MRpnzGUuc3CQARGo.png)

*Event-based Architecture*
- An architecture where communication is driven by events. Components interact by emitting and reacting to events, rather than direct method calls or data sharing.
- Flow of Control:
	- When an event is generated, it is sent to a central event bus.
	- Subscribers (interested components) listen for specific events and act upon receiving them.
	- Loose coupling between components — they don’t need to know about each other.

*Self-managing Architecture*
- A self-managing architecture enables components or systems to monitor, analyze, and control themselves with minimal human intervention


> [!note] Horizontal vs Vertical Distribution
> **Vertical distribution** means splitting different _functional layers_ of a system (like the app server and the database) onto different physical machines. Each machine handles a different role.
> **Horizontal distribution** involves spreading the _same layer_ across multiple machines. Each machine handles a part of the overall workload.