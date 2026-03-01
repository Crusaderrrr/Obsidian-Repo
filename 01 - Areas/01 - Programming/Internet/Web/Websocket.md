---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - internet
  - web
note type: Informational Note
---
# What is web socket?

This is a **protocol** like HTTP that provides data interchange simultaneously after any change. It is a server utility. 

*When it could be useful*:
- In group chats 
- In comments or likes
- Live score tables (sports, etc.)
- Online multiplayer games 

*How It works*:
1. **Handshake**
	- This is when the special HTTP request is sent from client to server and if server supports this type of connection it agrees.
2. **Open channel**
	- Once established, both client and server can send messages to each other at any time until the connection is closed.
3. **Full-Duplex**
	- Communication is bidirectional and simultaneous, unlike HTTP where each request must wait for the response.

