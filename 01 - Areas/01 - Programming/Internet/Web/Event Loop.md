---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - event_loop
  - JavaScript
  - browser
note type: Informational Note
---
*It is not the part of JavaScript* 
V8 engine is used in Node.js and in browser, but both have different event loops. 

Event loop is based on the [[Стек и Рекурсия|stack]], in few words it is like a stack of paper: we put papers one on another and then take them from the top. This system is called LIFO (last in first out). All the synchronous tasks go directly to the stack. 

**Web API**
Is used to declare event listeners and similar things. For example if we add two buttons (event listeners) both will be registered in web api and then, when action is executed this task will be put to *task queue* which is used for handling asynchronous actions. 

**Actually**, there are two task queues: 
- *Macrotask* queue (очередь событий)
	- Promises
	- queueMicrotask
	- [[Mutation Observer]]
- *Microtask* queue (очередь задач) priority
	- Timers (setTimeout, setInterval)
	- events (click, load, etc.)
	- Browser’s nuances (render, I/O, etc.)

Promises are always put in microtask queue. 
After finishing all the stack’s tasks, all the microtasks are resolved and then only one microtask, because inside this microtask could possibly be more macrotasks. 

**The queue is like that**:
1. Call stack
2. Microtask queue (all)
3. Macrotask queue (one)