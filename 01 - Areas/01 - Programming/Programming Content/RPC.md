**Remote Procedure Call**, is a communication protocol that lets a program execute a function on a remote server as if it were a local function call.

**Primarily** used for microservices interactions (*server-to-server*) not client-to-server, but can also be used that way.

## Workflow

1. The **client** calls its local **client stub** (looks like a normal function call)
2. The stub **marshals** (serializes) the parameters into a message
3. The message is sent over the network (TCP/IP or UDP) to the remote server
4. The **server stub** receives it, **unmarshals** the parameters, and executes the actual procedure
5. The result is serialized and sent back the same way
6. The client stub returns the result to the caller — as if it was all local​


# Types
- [[gRPC]]