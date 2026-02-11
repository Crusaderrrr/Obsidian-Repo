---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - web
note type: Informational Note
---
**General browser architecture**: 
![[IMG_1866.jpeg]]
*Consists of*: 
- UI - elements of the web page that user sees 
- Browser engine - depending on the UI actions interacts with rendering engine 
- Rendering engine - pases through stages of rendering. 
- Networking - assumes all the networking actions (DNS, packages interchange, etc)
- JS interpreter - makes so the js code works, connects interpreter, garbage collector, etc. uses [[V8 engine]]. 
- UI backend - handles API requests
- Data persistence - local storage of the browser 

**Chrome**: 
![[IMG_1867.jpeg]]

![[IMG_1868.jpeg]]

**Firefox**: 
![[IMG_1872.jpeg]]