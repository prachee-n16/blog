---
title: gRPC
---
RPC i.e. Remote Procedure Call is when client-server communications operate as if client API requests were a local operation or request was internal server code
- client sends a request to process on server which is always listening for remote server calls
- uses protocol like HTTP, TCP or UDP as data exchange mechanism

In gRPC, use Protocol Buffers and HTTP 2.0 for data transmission.
- OpenAPI requires developers to map RPC concepts to HTTP protocol
- gRPC abstracts HTTP communication

Data connections may be unary (one-to-one), server-streaming (one-to-many), client-streaming (many-to-one), or bidirectional streaming (many-to-many)