*Platform to process data as soon as it is available; i.e. stream processing*

Revolves around **events**, something that occurs at a particular point in time
- Events are continuously flowing, and in theory, infinite
- Concerns current state of system and entire log of events that happened before
	- pattern of capturing intermediate stages = **event sourcing**
- Events are immutable and time-stamped facts

In [[Event-driven Architecture|event-driven architecture]], communications happens via pub-sub model:
- traditionally, communication is through commands which trigger some action e.g. GET items for a page. 
	- reflects tight-coupling of server and client 
- however, events can be observed/reacted to by multiple systems
	- [[PubSub Model|publish-subscribe]] pattern allows for decoupled systems
		- allows for asynchronous reaction to data and more fault tolerant
- this line of thought is **event-first thinking**

> [!note] Queues
> Different from queuing systems like [[RabbitMQ]] 
> - once a message is processed, it is “popped” off the queue and unavailable to others, unless data is duplicated i.e. single-consumer model
> - similar to command-driven approach; producers write to specific location to trigger a task
> - in general, brokers take on extra "computational" burdens to be smart brokers (low throughput)

**Platforms**
- [[RedPanda]]
- [[Apache Kafka]]