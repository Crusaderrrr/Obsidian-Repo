---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
This the method like an f-string in python:
```java
String name = "Nikita";
char firstLetter = "N";
int age = 19;
double height = 187.1;
boolean isEmployed = false;

System.out.printf("Hello %s\n", name); 
System.out.printf("Your name satrts with %c\n", firstLetter); 
System.out.printf("You are %d years old\n", age); 
System.out.printf("You are %f cm tall\n", height); 
System.out.printf("Employed: %b\n", isEmployed); 
```

The schema looks like that:
`%[flags][width][.precision][specified-character]`

**Specified characters**:
- `s` - for string
- `c` - for char
- `d` - for int 
- `f` - for double
- `b` - for boolean

**Flags**:
- `+` - display a plus before a positive number: `+99.09`
- `,` - comma grouping separator for thousands 
- `(` - negative numbers are enclosed in `()`
- `space` -  display space before a positive number

**Width**:
- `0` - zero padding 
- `[number]` - right justified padding 
- `[negative-number]` - left justified padding 