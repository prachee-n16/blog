We will use the following design process:  
1. Scheduling (allocating operations to clock cycles)  
2. I/O allocation  
3. Initial high-level model  
4. Register allocation  
5. Datapath allocation  
6. Multiplexer insertion to connect datapath components  
7. Finite sate machine design  
8. Optimization

Assume we have a design problem with the following requirements
**Functional requirement**: output = (a x d) + c + (d x b) + b
**Performance requirement:**
- maximum clock period: 1 register delay + (2 addition delays or 1 multiply delay)
- maximum latency: 4 clock periods
**Resource requirement:**
- maximum of three inputs and one output
- maximum of two adders
- maximum of two multipliers
- unlimited registers

## Breakdown of Design Process
### Scheduling
Scheduling of the computation will require several steps:
1. Create a Data Dependency Graph
2. Schedule Operations into Clock Periods (as soon as possible schedule)
   - introduce a clock boundary when performance requirement will be exceeded
   - establishes lower bound on latency
3. Reschedule to Meet Signal Requirements
4. Fix Clock Period Violation
5. Optimize the Design
