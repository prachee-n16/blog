#### 4.1 Network Layer Services
- What are the two key network-layer functions?
	- Routing: Determine route taken by packets from source and destination
		- Use routing algorithms to determine next hop for the packet
	- Forwarding: Move packets from router's input to appropriate router's output
		- Use high performance hardware switching

#### 4.3 What is inside a router?
- What do routers repeatedly do to transfer packets?
	- First, they build and update routing tables using routing algorithms/protocols like RIP, OSPF, BGP
	- Next, they process the IP packets by (i) routing and finding next hop (ii) forwarding IP packets from incoming to outgoing link
- Draw the architecture diagram for a router
	- It is divided into two planes: data and control. 
		- Forwarding data plane is implemented in (decentralized) hardware
		- Routing and management control plane is (decentralized) software which makes routing decisions
![[Routing_Network_Layer.png]]

- Explain the function of router **input ports**
	- Line termination is a physical layer which handles bit-level reception; It refers to the process of receiving and conditioning incoming data signals from a physical communication link
	- Link layer protocol refers to Ethernet;
	- Finally, we implement a decentralized switching procedure where 
		- given an IP packet destination, we lookup the output port to send to using routing tables and start forwarding. This is a match plus action kind of behaviour
		- The goal is to perform input port processing at "line speed" where we complete match+action for one packet before the next one arrives
		- Otherwise, there's queuing: if IP packets arrive faster than forwarding rate into switch fabric
![[Input_Port_Routing.png]]

- Explain **switching fabrics**.
	- Switching fabrics (implemented in hardware) will transfer packets from input buffer to appropriate output buffers. 
	- The performance metric for switching fabrics is: **Switching rate** 
		- Rate at which packets can be transferred from inputs to outputs.
			- It is often measured as multiples of input/output line rate
			- N inputs: switching rate N times line rate desirable
		- So, if N = 5 and line rate = 1 Gbps then desirable switching rate = 5 Gbps

- Explain the three types of switching fabrics.
	- **Switching via memory**
		- Method used by first generation routers; traditional computers would switch under direct control of CPU
		- Packed will be copied to system's memory which means speed limited by memory bandwidth 
	- **Switching via bus**
		- Here, IP packets are moved from input port memory to output port memory via a shared bus
		- The issue with this method is:
			- bus contention where input ports will fight for access to bus
			- switching speed is limited by the bandwidth of bus
	- **Switching via interconnection network**
		- It uses "interconnection networks" which overcomes bus bandwidth limitations and designed for multiprocessor systems
![[Switching_Fabric_Types.png]]
- Explain the function of **output ports**
	- Buffering is required when datagrams arrive from fabric faster than transfer rate
	- Otherwise, IP packets can be lost due to congestion if there is a lack of buffers
	- Scheduling discipline: When there are multiple packets waiting in output queue, this strategy is used to decide the order in which queued packets are transmitted
![[Output_Port_Routing.png]]

#### 4.4 IP Packet (datagram) format
- Explain the Internet network layer.
![[Network_Layer_Outline.png]]
- Explain the IPv4 network format.
![[IP_Packet_Format.png]]
- Explain how IP fragmentation and reassembly works.
	- Links have a MTU (maximum transfer unit) attribute which is the largest possible link-level frame that can be sent on the link
	- So, a large IP packet (datagram) is fragmented by router where one IP packet becomes several IP packets
		- It is then reassembled only at destination. IP header bits are used to identify and reassemble related fragments:
			- Identifier (16 bits)
			- Flags (3 bits): (0 DF MF)
				- 0: first bit always zero (reserved)
				- DF: don't fragment (1)
				- MF: more fragments to follow (1)
			- Offset (13 bits) where in a fragment IP packet represents the position of the packet's first data byte in the data part of the original IP packet
	- Example provided in slide. 

#### 4.4 IP Addresses
- Explain the format of IP address in IPv4
	- The IP address is 32-bit long; It can be written in binary or dotted decimal notation where these are the same:
		- 10000001 01100001 01011100 00100101
		- 129.97.92.37
		- Conversion:
			- $(10000001)_2 = 129$
			- $(01100001)_2 = 97$
			- $(01011100)_2 = 92$
			- $(00100101)_2 = 37$
- What network elements have an IP address?
	- L2 switches and hubs do not have IP addresses.
	- End-devices such as laptop, servers etc. have one IP address.
	- Routers have multiple IP addresses; one for each physical interface.
- How do network elements get their IP address?
	- ICANN allocates IP address blocks to regional internet registries
	- A new ISP contacts its regional internet registry for a block of IP addresses
	- ICANN stands for Internet corporation for assigned names and numbers
- Explain the concept of network prefix
	- the portion of an IP address that identifies the network to which a device belongs
	- the rest of the bits are host ID;
- Explain classful vs. classless addressing?
	- Classful addressing is characterized by fixed length prefixes.
		- Class A: If the address begins with 0 and it is of form `prefix.host.host.host` (where prefix length is 8 bits)
		- Class B: If the address begins with 10 and it is of form `prefix.prefix.host.host` (where prefix length is 16 bits)
		- Class B: If the address begins with 110 and it is of form `prefix.prefix.prefix.host` (where prefix length is 24 bits)
		- Class D (begins with 1110) and E (begins with 11111)
	- Classless addressing 
		- CIDR: Classless InterDomain Routing where the subnet potion (prefix) in the address is arbitrary length 
			- VLSM - Variable Length Subnet mask 
		- e.g. 200.23.16.0/23 where subnet part is first 23 bits; host part is 9 bits
- Explain network ID and broadcast address
	- Network ID appears in routing tables; Individual host IP addresses don't
	- Broadcast address is used to perform IP-level broadcast
		- Sending IP packet with a broadcast address as the destination will send it to all nodes on the network
- Explain public IP address vs private IP address
	- For public IP addresses, 
		- these addresses are globally unique
		- routers everywhere can recognize them
		- any host can open a TCP connection with a machine with a public IP address
	- For private IP address
		- these are not globally unique
		- routers outside the organization do not recognize these
		- if a host has a private IP address, a host outside the organization cannot open a TCP connection with it
- How does an ISP get block of addresses?
	- ICANN: Internet Corporation for Assigned Names and Numbers
		- It allocates addresses, manages DNS and assigns domain names/resolves disputes
##### How do IP packets move from router to router?
- **Hop-by-Hop Routing**
	- Relies on **packet forwarding**; relaying of packets from one physical interface to another by routers on the Internet
	- A router chooses the next hop for a given packet P based on **table-driven routing**
		- Alternative forwarding technique: *Source routing*
			- The source host finds the path and puts it in the header, and sends the packet to the next router identified in the path. The "next" router looks at the path in the packet to further forward the packet
- **Routing Tables (RT)**
![[Routing_Table_Format.png]]
- **Prefix Matching**
	- If the destination net address (extracted from one entry of routing table) and destination IP address (extracted from IP packet) share $n$ most-significant bits, then matching occurs
	- If many matchings occur, there is a longest prefix matching
		- A longer prefix means smaller pool of IP addresses in the network
		- A smaller prefix means larger pool of IP addresses in the network
	- Packet forwarding based on longest prefix matching in each router will eventually deliver the IP packet to destination machine
	- There is the matching and forwarding algorithm:
```
inputs: 
- IP address from packet header (call it IP1)
- Routing Table (RT)

processing:
if (matching occurs between IP1 and RT) {
	- find the matching entry with the longest prefix
	- forward the packet via the appropriate interface
} 
else if (default entry exists in RT) {
	forward the packet via the appropriate interface
}
else {
	send error message (ICMP message) to the source of
	the packet
}
```

##### How do computers get an IP address?
- It can be hard-coded by system admin in a file. (Windows/UNIX methods covered in slides)
- Use DHCP (Dynamic host configuration protocol): dynamically gets address from as server
- **Explain DHCP**
	- The goal is to allows hosts to dynamically obtain its IP address from network server when it joins the network
		- It can "renew its lease" on the address in use
		- It also allows reuse of addresses that are currently inactive (regardless of history)
		- It provides support for mobile users who want to join the network
	- To give an overview of DHCP:
		- Optionally, the host broadcasts a **"DHCP discover"** message to locate any available DHCP servers on the network.
		- Optionally, DHCP server responds with a **"DHCP offer"** message.
		- The host replies with a **"DHCP request"** message to formally request the offered IP address.
		- The DHCP server sends a **"DHCP ack"** message to confirm the IP address assignment.

![[DHCP_Client_Server_Scenario.png]]
- **What does DHCP return?**
	- It returns the IP address of first-hop router for client i.e. default gateway
	- It returns the name and IP address of DNS server 
	- It returns the network mask

##### Address Aggregation
- Supernetting; It is a form of hierarchical addressing which allows efficient advertisement of routing information. 
- For example,
	- **Organizations (0, 1, 2, ... 7)** have their own IP address ranges, such as `200.23.16.0/23`, `200.23.18.0/23`, etc.
	- Without address aggregation, the router `R1` would need to advertise each of these address ranges individually
	- With address aggregation, `R1` can advertise a single summarized route `200.23.16.0/20` to represent all these networks. This means that `R1` tells other routers to "Send me anything with addresses beginning with `200.23.16.0/20`," simplifying routing decisions.
- When a router advertises a route, it is essentially saying, "I know how to reach this particular network or IP range, and I can forward packets to it." 
##### Network Address Translation
- Why do we need NAT?
	- A local network uses just one IP address as far as external agents are concerned
		- So, ISP does not need a range of addresses for each device; just one IP address for all devices
		- So, it can change addresses of devices in local network without telling anyone
		- ==So, it is possible to change the ISP or external IP address without altering the internal addresses of devices within the local network.== --> Why?
	- Devices inside the local network are not visible from the outside, providing an **extra layer of security** by hiding internal device IP addresses.
- Why is NAT controversial?
	- Routers should only process up to layer 3
		- NAT, however, requires routers to modify IP addresses and sometimes even port numbers, which extends processing beyond Layer 3 into **Layer 4** (the Transport Layer, where TCP/UDP ports are handled).
	- It violates end-to-end argument; NAT possibility must be taken into account by app designers for P2P applications
		- peer-to-peer apps; Applications like video calling, file sharing, or online gaming may struggle with NAT
	- address shortage should instead be solved by IPv6
		- NAT was originally adopted to address **IPv4 address exhaustion**—the limited number of available IPv4 addresses.
- Explain the NAT traversal problem; How to solve it?
	- When an external client wants to connect to a server located within a private, NATed network.
		- The server has a **private IP address** (`10.0.0.1`) that is only accessible within the local network.
		- The NAT router, which connects this local network to the internet, has one **public IP address** (`138.76.29.7`)
		- An external client (outside the local network) wants to connect to the server using the public IP.
		- However, the server’s address (`10.0.0.1`) is private and cannot be directly accessed by the client, as this IP address is not routable on the internet.
	- Solution 1: Statically configure NAT to forward incoming connection requests at given port to server
	- Solution 2: Universal Plug and Play (UPnP) Internet Gateway Device Protocol; Allows NATed host to learn public IP address and add/remove port mappings (with lease times)?
	- Solution 3: Relaying (used by Skype) where
		- NATed client establishes connection to relay
		- external client connects to relay
		- relay bridges packets between to connections
