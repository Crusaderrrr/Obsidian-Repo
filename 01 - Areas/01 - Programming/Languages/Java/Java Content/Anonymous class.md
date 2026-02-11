---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
- This is a class that does not have a name and cannot be reused.
- We can add a custom behavior without having to create a new class. 
- Often used for one time uses(TimerTask, Runnable, callback)

```java
Dog dog = Dog() {
	@Override
	void speak() {
		System.out.println("Something that dogs don't say");
	}
}
```