*[[Streaming data platform]]*, similar to [[Apache Kafka]]
- leverage [[PubSub Model|pub/sub]] model where communication hub is called **cluster**
	- cluster is made of one or more servers called **brokers** which mediate communication between producers and consumers
	- brokers also store data, organized into **topics** i.e. named stream or channel where related events are published
	- topics are divided into **partitions** - subset of topic data
	- when consumers are retrieving data from topics,
		- can work in groups i.e. consumer group to handle large message volumes
		- in each group, there is a group leader that handles partition assignments for each consumer

RedPanda stores events in a data-structure, log
- append-only that stores sequence of immutable records
	- when event is published, event is appended to end of partition log
	- position of record is represented as offset
- data is always ordered inherently
	- consumer reads data in order it is written

