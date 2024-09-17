End systems connect to the internet via access ISPs (internet service providers); and access ISP's in turn are interconnected which allows for two hosts to send packets to each other

**How do we connect million ISP's?**
- Option 1: connect each access ISP to every other access ISP
	- This does not scale; requires $O(N^2)$ connections for $N$ nodes
- Option 2: connect each access ISP to a global transit ISP
	- Customer and provider ISPs have some agreement
	- However, there will be competitors and the "global network" will break up into a cluster of routers
- Option 3: connect each access ISP to a global transit ISP; connect the competitor networks through **internet exchange points and peering links**
	- There also might be regional networks or content provider networks (e.g. Google/Microsoft)

![[Structure of the Internet.png]]