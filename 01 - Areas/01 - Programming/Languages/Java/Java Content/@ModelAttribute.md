---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
It is used to bind data between the web layer and the model, making the data available to views.

It can be used in two ways:
- **method parameters**
- **method itself**
---

When annotating *method parameters*:
- It binds request parameters (from inputs or query params) to a model object automatically
- Spring creates or retrieves the model object, populates its fields from the request data, and passes it to the controller method.

*Example*:
Code without @ModelAttribute
```java
@PostMapping()
public String create(@RequestParam("name") String name,
					@RequestParam("surname") String surname,
					@RequestParam("email") String email, 
					Model model) {
	Person person = new Person();
	person.setName(name);
	person.setSurname(surname);
	person.setEmail(email);
	// Добавляем человека в БД
	model.addAttribute(s: "person", person);
	return "successPage";
}
```

The same code, but using @ModelAttribute
```java
@PostMapping()
public String create(@ModelAttribute("person") Person person) {
	// Добавляем человека в БД
	return "successPage";
}
```

---

When annotating *methods itselves*:
- `@ModelAttribute` on a method defines that the method should add one or more attributes to the model.
- Such methods are typically used to prepare common model data that many views require, like dropdown options or shared reference data.

*For example*:
```java
@ModelAttribute("countries")
public List<String> populateCountries() {
    return List.of("USA", "UK", "Canada");
}
```
This adds a `countries` attribute to the model, available to any view rendered by the controller.