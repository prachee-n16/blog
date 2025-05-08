*software system where components on networked computers coordinate actions by passing messages*

The goals these systems need to meet are:
- **Be open** - easy to use and integrate in other systems; further defined by principles of:
	- *Interoperability* i.e. extent to which two different systems work with each other
	- *Composability* i.e. build larger systems by combining smaller, well-defined components
	- *Extensability* i.e. system can be easily enhanced with new features
	- *Separating policy from mechanism*, or separating `what we need to do` from `how we do it`
- **Be scalable**
	- Use techniques such as replication and partitioning to scale across geographically, # of users, and # of admins
- **Be distribution transparent** by making division of resources invisible to end users 
- **Allow for resource sharing**
- **Be secured**

The types of distributed systems we will be covering in this course:
1. High performance cluster (HPC)
	- Cluster computing 
	- Grid computing
2. Cloud computing
	- Content Delivery Networks
	- Geo-distributed database
3. Distributed information systems
	- Transaction processing
	- Enterprise application integration
4. Distributed pervasive systems
	- IoT
	- Sensor Networks

Related: [[Middleware]]