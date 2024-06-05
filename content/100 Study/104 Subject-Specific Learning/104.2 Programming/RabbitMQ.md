---
title: RabbitMQ
---
Popular open-source message queue software that is written in Erlang. It supports several API products such as AMQP, STOMP, MQTT and HTTP

1. Data transmission format
	- Binary protocols for data transfer which are really efficient, so lower network load
2. Connection handling
	- TCP to transport and existing connections can be reused for future communication, not the case for REST
3.  Message serialization
	- Protocol buffers increase the speed of communication by allowing more advanced serialization and de-serialization methods to be used for encoding and consuming the message content
4. Caching
	- No Caching, unlike REST
5. Load Balancing
	- Kubernetes, as a container orchestration solution, performs load balancing of HTTP/1.1 traffic without any adjustment in REST architecture
	- Asynchronous communication supports load balancing without further aids. The message broker itself takes the role of the load balancer, as it is capable of distributing requests to multiple instances of the same service.