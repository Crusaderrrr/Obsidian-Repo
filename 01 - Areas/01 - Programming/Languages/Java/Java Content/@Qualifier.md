---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
##  `@Qualifier`

This is used when ambiguity occurs (two or more beans found for dependency injection). 

Use **inside the constructor**:
```java
@Autowired
public MusicPlayer(@Qualifier("rockMusic") Music music1,
					@Qualifier("classicalMusic") Music music2) {
	this.music1 = music1;
	this.music2 = music2;					
}
```
