---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - linux
  - programming
note type: Informational Note
---
Linux is a modular OS and it has the next structure:
- **Kernel** - the core of the system that manages the CPU, memory, and device drivers. In summary, it is *responsible for low-level tasks*.
- **System Libraries** - These are reusable functions that *applications* rely on to perform system calls and *communicate with the kernel*. The most common set of libraries on Linux is the *GNU* C Library (glibc).
- **System Utilities and Daemons** - These include *essential commands*, *background processes*, and services that manage system tasks like *networking*, *printing*, and *user sessions*. Includes commands like: `ls`, `cp`, `bash`
- **Shell/Command Line face** - interprets user commands and scripts, lets user control the system.
- **User Space Applications** - software programs and graphical envs running on top of kernel, such as *browsers*, *editors*, etc. 

The graphical representation:
![[fundamental-architecture-of-linux.webp]]

# File System Hierarchy 
![[linux-filesystem-hierarchy.png]]
