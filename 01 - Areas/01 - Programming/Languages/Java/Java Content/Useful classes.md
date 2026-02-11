---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type:
---
1. [[User Input]]
2. **Random**
	Random int generation: `random.nextInt(0, 6)` - generates a random int from 0 to 6 *excluded*.
	Also there are methods like `.nextBoolean()`, `.nextDouble()`
3. **Math**
	PI and E constants are available with: `Math.PI` and `Math.E`
	`Math.pow(2, 3)` - $2^3$
	`Math.abs(-5)` - absolute (5)
	`Math.sqrt()` - square root 
	`Math.round()`
	`Math.floor()` or `Math.ceil()`
4. **Arrays**
	`.sort()`
	`.fill(arrayName, filler)` - fills the whole array with the filler
5. **Wrappers**
	These are used to make variables behave as objects.
6. **ArrayList**
	This is basically a Python list.
7. **Collections**
8. **FileWriter**
9. **BufferedReader**
10. **FileReader**
11. **AudioInputStream**
12. **LocalDate**, **LocalTime**, **LocalDateTime**
	Used to work with date and time, UTC format, could be custom formatted. 
13. **Timer**
	A class that schedules tasks at specific times or periodically.
	*Useful for*: sending notifications, scheduled updates, repetitive actions.
	**TimerTask**
		Represents a task that will be executed by the Timer. To do so we need to extend a TimerTask class to define your task and create a subclass of TimerTask and @Override run(). 
```java
Timer timer = new Timer();
TimerTask task = new TimerTask(){
	@Override
	public void run() {
		System.out.println("Hello");
	}
}
timer.schedule(task, 0, 1000); // task, delay, period
```

14. **HashMap** (K, V can be of any type)
```java
HashMap<K, V> map = new HashMap<>();

map.put(); //add
map.remove(); //delete
map.get(key);
map.containsKey();
map.containsValue();
map.keySet();
```
