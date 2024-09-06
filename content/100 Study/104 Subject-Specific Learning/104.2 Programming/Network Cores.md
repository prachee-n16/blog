It is a mesh of interconnected routers.
- There are two key network-core functions
	- Routing a packet means finding the next hop router for the packet; done with routing algorithm
		- The routing algorithm maintains some form of a routing table to facilitate process
	- Forwarding a packet means moving packets from router's input to appropriate router output
		- It is internally moved by setting the destination address in the arriving packet's header
- The key question when dealing with network cores: **How is data moved through the core routers?**
	- we use [[Packet Switching|packet switching]], where a router receives a packet; the router makes a decision to forward the packet to a next router
	- the counterpart of packet switching is [[Circuit Switching|*circuit switching*]]: when a router received a packet; the router does not make any decision.
		- packets are routed along a defined path (i.e. circuit) before sending packets

> [!note] Packet switching vs. Circuit switching
> 
> Packet switching is good because:
> - it allows for resource sharing
> - it is simpler with no call setup
>   
> However, on the other hand
> - it is possible for excessive congestion which results in packet delay and loss
> 	- [[protocols]] are needed for reliable data transfer and congestion control
> 
> Example: Consider a 1 Mb/s link where each user gets 100 kb/s when active and it's active 10% of the time
> - With **circuit switching**, it supports 10 users (= 1 Mbps/ 100 kbps)
> - With **packet switching**, it supports 35 users who are active 10% of time.
> 	- probability of the number of active users greater than 10 at the same time is less than .0004.
