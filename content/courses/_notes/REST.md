---
title: REST
---
Representational State Transfer is a software architecture style 
- REST compliant systems are called RESTful
- Characterized by the fact that they are stateless
	- Stateless app does not retain information about the user's previous interactions 
	- "Statelessness" is when the server does not need to know about what state the client is in and vice-versa
- Separates the concerns of the server and client
	- Implementation of both parties can be done separately
	- The only thing that matters is that they know what format to send messages to each other
		- Hit same REST endpoints, perform same actions and receive same responses

REST works as follows:
- The client makes a request to create, modify or delete a resource on the server
- The request contains the resource endpoint and may also include additional parameters
- The server responds, returning the entire resource to the client once the operation is complete
- The response contains data in JSON format and status codes

