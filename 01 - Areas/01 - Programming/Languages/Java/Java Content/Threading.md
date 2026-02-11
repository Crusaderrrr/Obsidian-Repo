---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
Allows a program to run multiple tasks simultaneously.

# Creating a Thread

**Option 1**:
Extending the Thread class

**Option 2**:
Implement a runnable interface.
1. **Create a class that implements Runnable interface**  
    Define a class that implements the `Runnable` interface. This interface has a single method `run()` that you need to override. The code you want the thread to execute goes inside this `run()` method.
    
2. **Implement the `run()` method**  
    Inside the `run()` method, put the code that should run in a separate thread. For example, printing a message or some task-specific logic.
    
3. **Create an instance of your Runnable class**  
    Instantiate the class that implements `Runnable`.
    
4. **Create a Thread object passing the Runnable instance**  
    Use the `Thread` class constructor and pass your `Runnable` instance as an argument.
    
5. **Start the thread by calling `start()` on the Thread object**  
    Call the `start()` method on the `Thread` object to create a new thread and begin executing the `run()` method in parallel with the main thread*.*

*Example code*:
```java
public class MyRunnable implements Runnable { 
	@Override 
	public void run() { 
		System.out.println("Thread running: " + Thread.currentThread().getName()); 
	} 
	public static void main(String[] args) { 
		System.out.println("Main thread: " + Thread.currentThread().getName()); // Step 3: Create instance of Runnable 
		MyRunnable runnable = new MyRunnable(); // Step 4: Create thread passing Runnable instance 
		Thread thread = new Thread(runnable); // Step 5: Start the thread 
		thread.start(); 
	} 
}
```

To enable **multithreading** simply add more Thread instances.

# Synchronization 

If we have two or more threads, and we need them to be executed in special order, we need to use a keyword: **synchronized**.

There are two use cases:
1. *On the method*
```java
sychronized void methodName() {
	//code
}
```

2. *On the code block*
```java
sychronized (this) {
	//code
}
```

It makes the threads act in the order they were called.