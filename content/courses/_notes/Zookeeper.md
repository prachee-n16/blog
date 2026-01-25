*coordinates and manages distributed applications*
- **ZooKeeper Ensemble**: A group of ZooKeeper servers that work together to maintain a distributed configuration service.
- **ZNodes**: Hierarchical nodes in ZooKeeper's namespace, akin to files and directories in a file system
	- **Persistent ZNodes**: Remain in the system until explicitly deleted
	- **Ephemeral ZNodes**: Exist only as long as the session that created them is active
- **Sessions**: A client connection to ZooKeeper. Sessions are transient and can expire.
- **Watches**: Mechanism for clients to get notifications of changes to ZNodes.

**Architecture**:
- **Leader**: One ZooKeeper server in the ensemble acts as the leader, handling write requests and synchronizing the state across followers.
- **Followers**: Other servers in the ensemble that receive updates from the leader and can handle read requests.
- **Quorum**: A majority of the servers (more than half) in the ensemble must agree on updates to maintain consistency.

**Integration with Kafka**:
- **Broker Metadata Management**: ZooKeeper manages Kafka broker metadata and cluster configurations.
- **Controller Election**: Kafka uses ZooKeeper to elect a controller that handles partition leader elections.
- **Topic and Partition Management**: ZooKeeper stores metadata about Kafka topics and partitions.
