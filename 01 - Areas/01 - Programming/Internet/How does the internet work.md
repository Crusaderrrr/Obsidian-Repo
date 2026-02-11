#programming #internet 

## Introduction
What a *Network* is?
The network is a group of computers or other devices which are connected to each other. It can be a network of your devices, network of your neighbor’s devices connected, network of your friend. All these networks connected form the *internet*.
>[!info] The internet is a network of networks.

  

## How the internet works: overview
It works by connecting devices using some standardized protocols, that provide security and reliability.
The core of the internet is a system of interconnected routers. Devices that transmit information. This information is transmitted in packages.
Most common *protocols* are:
- **IP** (Internet Protocol)
    This protocol is responsible for routing packages to the correct destination.
- **TCP** (Transmission Control Protocol)
     Ensures that packages are transmitted reliably and in correct order.  

Other protocols:
- **DNS** (Domain Name System)
- **HTTP** (Hypertext Transfer Protocol)
- **SSL/TLS** (Secure Sockets Layer/Transport Layer Security)

## HTTP and HTTPS Protocols

**HTTP** (Hypertext Transfer Protocol) provides a connection between user and server. User, when requesting data, sends this request to a server and then servers sends response with requested data.

**HTTPS** (HTTP Secure) is a same protocol but that one provides a protected connection. It encrypts data before transmit it between client and server SSL/TLS (Secure Socket Layer/Transport Layer Security). It is more popular than HTTP.

## OSI/ISO vs TCP/IP
![[Pasted image 20250811112535.png]]
- **OSI (Open Systems Interconnection)** is a conceptual framework developed by the **International Organization for Standardization** (**ISO**) in the 1980s to standardize how computer systems connect and communicate over networks.
- The **TCP/IP model** is the foundation of the modern Internet, describing practical protocols used for real-world networking. It has **four layers**

## Ports 
![[Pasted image 20250811124155.png]]
1. **The Client (Your Computer)**
    - When you send a request to a server (in this case, an **Nginx** web server), your operating system creates a **source port** on your machine.
    - This **source port** is a temporary, randomly selected number from a range called the **ephemeral port range**.
    - In the image, the source port is **49153**.
2. **The Server (Nginx)**
    - The server listens on a **destination port**, in this case port **80**, which is the standard port for HTTP traffic.
3. **Ephemeral Port Range (49152–65535)**
    - This range is reserved for temporary communication ports used by clients (your machine) when starting outbound connections.
    - Your operating system picks one from this range each time you initiate a TCP connection.
    - This is how your computer uniquely identifies multiple simultaneous connections — even to the same server.
4. **Why This Matters**
    - When the server responds, it sends the response **to your IP and the source port you originally used**.
    - Your OS uses this port number to deliver the data to the correct application process (for example, your web browser tab that made the request).