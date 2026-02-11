---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
This is how controllers pass data to view (Thymeleaf).

In our controller we need to define model and then define data to pass.

```java
@GetMapping("/hello")
public String helloPage(@RequestParam(...), @RequestParam(...), Model model) {
	model.addAttribute("message", "Hello, " + name + " " + surname);
	return "hello";
}
```

This means that we add a String ("Hello, ...") to a component `message` of the html page.