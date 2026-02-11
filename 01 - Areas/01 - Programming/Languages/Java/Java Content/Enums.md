---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
A special class that is just a list of constants.
It enhances the structure of the code.

```java
public enum Day {
	SUNDAY(1), MONDAY(2), TUSEDAY(3), WEDNSDAY(4), THURSDAY(5)...;

	private final int dayNumber;

	Day(int dayNumber) {
		this.dayNumber = dayNumber;
	}

	public int getDayNumber(){
		return this.dayNumber;
	}
}

// IN other class:
Day day = Day.SUNDAY;
```

It is more efficient to use Enums, rather than strings.