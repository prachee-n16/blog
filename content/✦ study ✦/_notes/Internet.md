Internet is a collection of thousands of Internet Service Providers or ISPs. They work together to provide global connection. 
- ISPs are a collection of small autonomous systems or AS. This can include the following components:
	- **Access Network**: Provides connectivity to end users and devices, typically at a local level.
	- **Distribution Network**: Manages traffic between the access network and the core network, ensuring efficient routing and load balancing.
	- **Core Network**: The backbone of the ISP, providing high-speed, large-scale connectivity both within the ISP and to other networks.
	- **DHCP Server (Dynamic Host Configuration Protocol)**: Allocates IP addresses dynamically to devices within the network.
	- **DNS Server (Domain Name System)**: Resolves human-readable domain names (e.g., [www.example.com](http://www.example.com)) into IP addresses that devices use to route data.
	- **[[Protocols]]**

![[Internet.png]]*Breakdown*:
- Access Network: providing connectivity to homes and businesses (end users)
	- connects the user's device to the ISP's distribution network
	- handles local network traffic and is where services like DHCP (Dynamic Host Configuration Protocol) and DNS (Domain Name System) operate to assign IP addresses and resolve domain names
- Distribution Network: represented by several routers
	- connects the access network to the core network (load balancing)
- Core Network: backbone of the ISP's infrastructure
	- enforces security and connectivity policies
- Regional ISP:  layer connects the ISP's core network to other ISPs or a regional network
- Global ISP: lowest layer; representing the global internet infrastructure