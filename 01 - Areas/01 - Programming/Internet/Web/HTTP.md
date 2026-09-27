**HTTP** (Hypertext Transfer Protocol) provides a connection between user and server. User, when requesting data, sends this request to a server and then servers sends response with requested data.

**HTTPS** (HTTP Secure) is a same protocol but that one provides a protected connection. It encrypts data before transmit it between client and server SSL/TLS (Secure Socket Layer/Transport Layer Security). It is more popular than HTTP.

*Key parts of HTTP request*: 
- **Start line** `GET /users/123?active=true HTTP/1.1`
- **Headers**, with this structure `Name: value`. One per line
- **Body**, can be JSON, HTML, protobuf, etc.

The *response* has the same structure, only the first line differs `HTTP/1.1 200 OK`.