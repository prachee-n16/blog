
**Terms and Definitions**
Medium of interconnection: a medium is needed to interconnect group of computers or router with computer
- Medium is needed to move electrical signals from transmitter to receiver
- The media can be wired or wireless, with two types: broadcast medium or point-to-point medium
	- Broadcast: in this medium, signal from one node reaches all other nodes
- Note: medium is singular, media is plural

**Characteristics of Media**
- **Frame**: Moving bit by bit in a pipelined fashion from transmitter to receiver
	- each bit occupies some space on the medium to prevent collision
- Bits take non-zero time to propagate from transmitter to receiver. So, we calculate **rate of transmission**, **transmission delay** and **propagation delay**
	- Rate of transmission/Bandwidth: $T_x$ rate is total number of bits put by a transmitter on the medium in 1s
	- Transmission delay: Time taken by transmitter to put entire frame on medium
	  $\text{Transmission delay} = \frac{\text{Length of frame (bits)}}{\text{Transmission rate (bps)}}$
		- Note: Kbps = $10^3 $bps; Mbps = $10^6$ bps; Gbps = $10^9$ bps
	- Propagation Delay: time taken by a bit to move from transmitter to receiver
	  $\text{Propagation delay} = \frac{\text{Distance between } T_x \text{ and } R_x \text{ [m]}}{\text{Speed (m/s)}}$ 
- Bits are corrupted moving from transmitter to receiver; this bit corruption property of a medium is expressed as **BER (bit error rate)**
	- $\text{BER} = \frac{\text{\# of bits corrupted}}{\text{total \# of bits transmitted}}$

- Data communication happens in chunk of bits; we send multiple bits rather than a single bit. In different layer of [[protocols]], these chunk of bits are called differently:

| Layer of Protocol                | Term    |
| -------------------------------- | ------- |
| Application Layer                | Message |
| Transport Layer                  | Segment |
| Network Layer                    | Packet  |
| Medium Access Control (MAC/Link) | Frame   |
| Physical Layer                   | Frame   |
- the generic term is PDU (protocol data unit) where message is Application Layer PDU
	- Structurally, all PDU starts with a header, followed by data to transfer
	- More about **frame**/**packet**: 
		- structured sequence of bits that enables transmitter and receiver to communicate
		- they are expressed in bytes and lengths are capped by MTU (Max Transfer Units)
			- Why? buffer allocation, memory management etc.

**LAN and WLAN**
- LAN: interconnection of a set of computers by means of a single wired, broadcast medium
- WLAN: interconnection of a set of computers by means of a single wireless, broadcast medium
	- Difference between LAN and WLAN is slightly more than just being wired and wireless; revisit later after discussing how the Internet works?

**Terms and Definitions**
- **Model of time**: There are two models of time in relation to when information is transferred by a receiver
	- Continuous time: In this model, a node can start transmitting at any time
	- Slotted time: In this model, a node can start transmitting only at the beginning of a time slot and transmission can not overrun a slot
- Communication directions
	- **Full duplex:** In full duplex communication, a node can transmit a frame and receive a frame exactly at the same time
	- **Half Duplex:** in half duplex communication, a node can either transmit a frame or receive a frame at any given instant
