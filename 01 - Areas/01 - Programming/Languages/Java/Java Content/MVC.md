---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
*The structure*
![[Pasted image 20250821131046.png]]

1. **Controller**
	- Processes user requests 
	- Interchanges data with *model*
	- Shows user a correct performance
	- Redirects user 
	- etc.
2. **Model**
	- Stores data
	- Interacts with DB
	- Gives data from controller to view
3. **View**
	- Receives data from controller and displays it in browser
	- For dynamic displaying *templators* are used
---
# Structure of MVC
- Consists of Java classes (controllers, models, etc.), annotations such as @Controller
- Kit of HTML pages, often with JS code.
- Spring configuration (XML, annotations or Java)