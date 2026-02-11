---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - internet
note type: Informational Note
---
1. **URL Parsing**  
    The browser first parses the URL you typed to identify the domain name (e.g., [www.example.com](http://www.example.com/)).

2. **DNS Lookup (Domain Name System)**  
    Since computers communicate over the internet using IP addresses, the browser needs the IP address of the website server. To get it, the browser asks a DNS resolver to translate the human-readable domain name into an IP address. This involves:
    - Checking the browser cache to see if the IP is already known.
    - If not cached, the DNS resolver queries a chain of DNS servers:
        - **Root DNS server** (knows top-level domains like .com)
        - **TLD DNS server** (knows authoritative servers for domains ending in .com, .org, etc.)
        - **Authoritative DNS server** (knows the exact IP address of the requested domain)
    - The IP address is returned to the browser, often in milliseconds.

3. **Establishing a Connection**  
    Using the IP address, the browser opens a connection to the web server. Most commonly, this is done via the **TCP protocol**:
    - The browser initiates a **TCP handshake** with the server, which involves exchanging messages to establish a reliable connection.
    - The server listens on a specific **port** (usually port 80 for HTTP or 443 for HTTPS).

4. **HTTPS/TLS Handshake (if applicable)**  
    If you are accessing a secure website (HTTPS), an additional handshake happens to establish encrypted communication using TLS (Transport Layer Security).
    
5. **HTTP Request**  
    After the connection is established, your browser sends an HTTP GET request asking the server to send the webpage content.
    
6. **Server Response**  
    The server processes the request and sends back the webpage data, usually HTML, CSS, JavaScript, images, etc.
    
7. **Rendering the Page**  
    The browser renders the webpage on your screen by interpreting the received data, making additional requests for embedded resources as needed.
    
8. **Closing or Reusing the Connection**  
    Depending on the protocol version and settings, the TCP connection may be kept alive for further requests or closed.