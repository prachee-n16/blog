*Distributed event streaming platform by Linkedin*

Core concepts, some covered in [[RedPanda]] already 
- **Producer**: Publishes messages to Kafka topics.
- **Consumer**: Subscribes to topics and processes messages.
- **Topic**: Logical channel to which messages are sent by producers and from which messages are read by consumers.
- **Partition**: Topics are split into partitions for scalability and parallelism.
- **Broker**: Server in a Kafka cluster, responsible for storing data and serving client requests.
- **Cluster**: Group of brokers working together to provide high availability and fault tolerance.

**Architecture**:
- **Publish-Subscribe Messaging System**: Allows decoupling of data streams and processing applications.
- **Log-based Storage**: Messages are stored in the order they are received.
- **Scalability**: Easily scalable by adding more brokers and partitions.
- **Fault Tolerance**: Data replication across multiple brokers.

**Data Flow**:
- Producers send messages to specific topics.
- Messages are distributed across partitions.
- Consumers read messages from topics (or specific partitions).
- Offsets track the position of the consumer in the log.

**Administration**:
- Monitoring with tools like Prometheus, Grafana, and Confluent Control Center.
- [[Zookeeper]] (deprecated in newer versions) for coordinating and managing Kafka cluster.
