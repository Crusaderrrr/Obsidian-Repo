---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
  - thymeleaf
note type: Informational Note
---
This is a server-side template engine used for processing and creating HTML, XML, CSS JavaScript and plain text.

*BEFORE*, the methods below we need to define and `addAtribute()` to the model that we are gonna use.

## Information flow
This is how the data flows with Thymeleaf:
1. Creation of the model object
2. Population of this object with data from form fields
3. Sending of the object to the controller 
4. Managing data

**Methods**:
- `<th:text="${person.getName()}">`
- `<th:each="person : ${people}">` - makes some kind of a Stream that can be iterated.
- `th:herf="@{/people/{id}(id=${person.getId()})}` - redirects to the `/people/:id`, id got from person Object.

# Forms 
Thymeleaf is used to model forms also.
**Main attributes**:
- `th:method` - used to specify the method that is gonna be used when submitting a form (GET, POST, PATCH, etc.), this attribute solves the famous *form issue*, because in HTML5 forms have only two methods: POST and GET.
- `th:action` - used to specify the *form submission URL*.
- `th:object` - defines what model object will be created and passed to the controller after form submission. The flow is explained above.
	- `th:field` - It binds HTML form field to a property of the object specified by the `th:object`


## Form Validation
For this we need a `Hibernate Validator` dependency.

**How to use?**
Inside a defined Model we can add annotations to a model properties (name, age, email, etc.). These are:
- `@NotEmpty`
- `@Email`
- `@Min`
- `@Size`
and more. 

*after that* to enable validation we need to add `@Valid` annotation inside the controller's Mappings before a model definition and define a **BindingResult** (object where errors will be stored) strictly after the model:
```java
  @PostMapping()
  public String create(@ModelAttribute("person") @Valid Person person, BindingResult bindingResult) {
    if (bindingResult.hasErrors())
      return "people/new";

    personDAO.save(person);
    return "redirect:/people";
  }
```

Also the view html file should be enhanced with a div element, where error message will be displayed.