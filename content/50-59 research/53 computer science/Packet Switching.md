Process involves breaking down application-layer messages into smaller units called packets before they are sent over a network
- Forward packets from one router to next, across links on the path from source to destination
- Each packet is transmitted at full speed of the link

**Store and forward**
Imagine it takes $\frac{L}{R}$ seconds to transmit a L-bit packet into the link at R bits per seconds.

Here, the entire packet must arrive at the router before it is transmitted to next link
- Router needs the packet header before it forwards the packet
- It also allows you to ensure we don't forward a corrupted packet
So, the end to end delay is $2\frac{L}{R}$, assuming zero propagation delay.

**Queuing delay and Loss**
- If arrival rate in bits to link exceeds transmission rate of link for a period of time
	- packets will queue, waiting to be transmitted and could be lost if the buffer memory fills up

There is an effort to provide circuit-like behaviour (i.e. bandwidth guarantees that are needed for audio/video apps) which still remains an unsolved problem