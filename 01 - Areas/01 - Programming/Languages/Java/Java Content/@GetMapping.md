---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
Represents GET request.

There are two parameters of this method:
- *HttpServletRequest*
```java
@GetMapping("/hello")
public String helloPage(HttpServletRequest request) {
	String name = request.getParameter( s: "name");
	// Работаем с пришедшим от пользователя параметром
	return "first/hello";
}
```

- *@RequestMapping* 
```java
@GetMapping("/hello")
public String helloPage(@RequestParam("name")\String name){
	// Работаем с пришедшим от пользователя параметром
	return "first/hello";
}
```

Both of them **extract name parameter of the URL**.