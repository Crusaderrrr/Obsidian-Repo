---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - web
note type: Informational Note
---
**TCP/IP model is another model of data transmition**. This is the real model that is used all over the internet. It has 4 layers:

1. *Application*
	Handles high-level protocols for user applications and services, providing a platform-independent interface. Protocols are: HTTP, HTTPS, FTP, SMTP, DNS, etc.
2. *Transport*
	Manages end-to-end communication, data segmentation, flow control, and error checking between devices.
3. *Internet*
	Responsible for logical addressing (IP addresses), routing packets across networks, fragmentation, and packet forwarding. The data is transferred via routers.
4. *Network Access Layer*
	Combines physical and data link functions for hardware-level transmission over local networks. Uses MAC addresses for device identification, formats data into frames (e.g., Ethernet), and transmits bits via cables, Wi-Fi, or switches.