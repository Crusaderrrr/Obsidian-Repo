---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - java
  - programming
note type: Informational Note
---
Memory in Java is divided in 2 parts: 
- **Stack** 
	- Variables are stored here 
	- Also values of primary types are stored here (int, double) except *String* 
	- Object references 
- **Heap**
	- The objects themselves 
	- Strings in *String pool*
	- The minimal and maximum size can be changed within the command line `-Xms ` and `-Xmx`

### Garbage Collector 

This is a special mechanism in JVM which deletes the objects and strings from the heap that do not have a reference. 

- We can barely control it (only ask to review)
- There is an hierarchy of the variables, which helps with optimization: 
	- Eden - are gonna be deleted 
	- S0 - survivors 
	- S1 - survivors 
	- Tenured 
	- Permanent Generation (perm gen)
