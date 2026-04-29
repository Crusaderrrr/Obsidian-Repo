This is a pattern **should be used when a class should have a single instance available**. It disables all means of creating objects of a class except for the special static creation method.

*The most basic example*: 
```java
public class Singleton {
	private static Singleton instance;
	private String data;
	
	private Singleton(String data) {
		this.data = data;
	}
	
	public static Singleton getInstance(String data) {
		if (isntance == null) {
			instance = new Singleton(data);
		}
		return instance;
	}
}
```

*Thread safe and optimized version*:
```java
public class Singleton {
	private static volatile Singleton instance;
	private String data;
	
	private Singleton(String data) {
		this.data = data;
	}
	
	public static Singleton getInstance(String data) {
		Singleton result = instance;
		if (result == null) {
			synchronized (Singleton.class) {
			result = instance;
				if (result == null) {
					isntance = result = new Singleton(data);
				}
			}
		}
		return instance;
	}
}
```


### Use cases:
- Database connection (too expensive for many connections)
- Logger
- App Configuration
- Hardware Access