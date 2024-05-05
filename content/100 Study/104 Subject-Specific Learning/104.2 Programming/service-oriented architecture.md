---
title: SOA
---
*Service-Oriented Architecture*

It is an architecture style that focuses on discrete services instead of a monolithic design. 
- It is a way of thinking about services and service-based development based on the outcome of services.
- Service is a discrete of functionality that can be accessed and updated independently.
	- Logically represents a "repeatable" business activity with a specified outcome
	- Self-contained
	- Black box for consumers (i.e. not aware of inner workings)
	- May be composed of other services

This architecture can be implemented with web services or micro-services. Why? This means each service is accessible over internet, independent of what platform or programming language they use. SOA can be built using any service-based technology:
- [[soap|SOAP]]
- [[rest|REST]] 
- [[grpc|gRPC]]

Architectures can operate using wide range of technologies:
- Web services based on SOAP
- Messaging with [[rabbitMQ]]
- RESTful HTTP
- gRPC

Extensions include: [[eventDrivenArch|Event-driven Architecture]], API, Web 2.0, Microservices