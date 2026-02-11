---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - web
note type: Informational Note
---
**Open Systems Interconnections**, which is a model of how data is transmitted between devices. This model is used primarily for **educational purposes**. Consists of 7 layers:

1. *Physical layer*
	Transmits raw bitstreams via cables, which are good transmitters.
2. *Data layer* 
	Handles framing via switches (коммутаторы) and addressing (both, sender and receiver have theirs unique <mark style="background: #ABF7F7A6;">Mac Addresses</mark>). Bits -> frames. 
3. *Network*
	Manages logical addressing and routing. A device called router is needed here, which interconnects local devices with the hole internet. <mark style="background: #ABF7F7A6;">Packages</mark> are being transmitted here. Also, the *ARP* (Address Resolution Protocol) is used here.
4. *Transport*
	Ensures complete data transfer, segmentation, error recovery and flow control via <mark style="background: #ABF7F7A6;">TCP/UDP</mark> (Transmition Control Protocol/User Datagram Protocol)
5. *Session*
	Establishes, maintains and terminates communication sessions.
6. *Presentation*
	Translates data format, encryption and compression. When we send a .`jpg` pic to our friend, this layer is responsible for translating the data back to the original format.
7. *Application*
	This layer is responsible for protocol management (HTTP, HTTPS, SMTP, POP, etc.) This is the closest to the user layer.

## Important

**The information that we send is passed through this model twice, on send and on receive**. A good [video](https://www.youtube.com/watch?v=wnxDXj2Fqus&t=1s).