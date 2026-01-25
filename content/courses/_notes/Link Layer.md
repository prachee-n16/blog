*Layer 2 on the OSI model;*

**Terminology**
- Nodes: These are hosts, routers etc. on the link layer.
- Links: Communication paths set between physically adjacent nodes in the link layer;
- Frame: Layer 2 PDU (Protocol Data Unit); encapsulated datagram 

**Services**
1. Framing: It encapsulates the network layer datagram with header fields; 
2. Link Access: MAC Protocol provides control to when/how packets are sent when a link is shared with multiple transmitters. 
	- In the case of a single transmitter and receiver, the protocol is simple: send packet if link is not busy.
3. Reliable delivery: Not a service for low bit-error links (e.g. wired connections) but important for high bit-error links e.g. wireless connections
4. [[Error detection]]: Errors can be caused by signal attenuation or noise. The receiver should be able to detect errors in the frame, if any.
5. Error correction: If errors are detected, receivers should identify where and correct the error without resorting to retransmission.
6. Half-duplex and Full-duplex
	- If it's half-duplex, the link can either be transmitting or receiving a packet.
	- If it's full-duplex, the link can simultaneously have transmitting and receiving of packets.
7. Flow control: Pacing between transmitting adjacent packets to ensure no interference.

**Implementation**
It is combination of hardware and software.
- The NIC, or network interface card is a hardware chip that controls most of the services: framing, error detection, error correction etc.
- When sending the frame, it takes the network datagram (stored in higher layers of the protocol stack) and encapsulates it in a link layer frame (filling fields e.g. the datagram, headers, ED information etc.)
	- Requires software to control hardware operations; high-level operations.
- When receiving the frame, it retrieves the original network datagram from link layer frame and checks for errors (corrects it if need be);
	- Requires software interrupts upon packet arrival;