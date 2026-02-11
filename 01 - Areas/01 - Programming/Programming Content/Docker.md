---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - docker
note type: Informational Note
---
This tool is used for [[Виртуализация|Virtualization]].
Basically, it makes easier the process of deployment of the applications to the servers.
A good explanatory [video](https://youtu.be/lr1rYnUubpQ?si=6Z32X7KlvHJhv6p8).

Its **key parts** are:
- *Images* - those are templates of the full application. Consist of the files, os setups, commands that should be run to start the application, etc.
	- *Image Registry* - `DockerHub`, it is a cloud storage for the images, from where the image can be deployed. Also, it has a <mark style="background: #BBFABBA6;">pre-built images</mark>, for Postgres, Node, etc.
- *Container* - concrete launched/deployed application based on the image. These are lightweight (have a partial OS, only necessary components)
- *Docker Network* - a network that lets containers communicate, it defines how containers get IP, how trafic flows between them, etc.
- *Docker Compose* - tool that lets run multicontainer applications and simplifies the adjustment part, it's a `.yml` file.  