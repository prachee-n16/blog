These are distributed algorithms that determine how nodes share a channel. It achieves this by determining when a node can transmit to reduce frame collisions.

> [!note] **Ideal Multiple Access Protocol**
> Given a broadcast channel of rate R bps, we would ideally want:
> - **peak rate**: when one node wants to transmit, it can send at rate R
> - **long term average rate**: when M nodes share a medium, each node gets an average rate of R/M bps.
> - **fully decentralized**: there is no central controller to coordinate transmission/no synchronization of clocks or slots
> - **simple**: low computation time with plug-and-play nature

The three broad classes of MAC protocols
1. [[MAC Protocol - Channel partitioning|Channel partitioning]]
2. [[MAC Protocol - Random access|Random access]]
3. [[MAC Protocol - Taking turns|Taking turns]]

An [[L2 Switches, L1 Switches and Connectors|L2 switch / connector ]](Layer 2, Data Link layer) comes into play any time devices need to forward traffic based on MAC addresses within the same network segment, before routing decisions based on IP addresses (Layer 3) are required.