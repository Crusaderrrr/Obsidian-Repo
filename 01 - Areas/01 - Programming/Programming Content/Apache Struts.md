**Struts** 2 is the maintained version, but in general it is a legacy **Java MVC Framework** that is now completely replaced by [[Spring MVC]].

### Main concepts 
- **Action** - is a Java class with methods that should return a String like "success", "error", "redirect", etc. Based on the response Struts decides what to do, in most cases (success, error) it just servers `.jsp` file.
	- `new` Action for EACH request
	- Action has fields that can be set upon creation
- **JSP** - *Java Server Pages*, which is an HTML page with OGNL expressions inside, that is server-rendered (built server side and returned as a response).
- **OGNL** -  *Object-Graph Navigation Language*, basically offers a comfortable way to call methods or access data from Action instances directly in the HTML.
	- e.g. `<s:property value="%{unitid}"/>`

### How a request flows
1. `StrutsPrepareAndExecuteFilter` is a servlet filter that catches incoming requests. It plays the role of Spring’s `DispatcherServlet`.
2. `struts.xml` (or annotations) maps a URL to an Action class and method.
3. The **interceptor stack** runs before and after the action. It handles parameter binding, validation, file upload, and exceptions. This is close to Spring’s `HandlerInterceptor` combined with filters, but in Struts _most core features_ are interceptors. Parameter binding itself is just the `params` interceptor.
4. The **Action** executes and returns a plain **String result code**, such as `"success"` or `"input"`.
5. The **Result** maps that code to a view: usually a JSP or FreeMarker template, or a redirect or JSON.


### Example of Action binding

**struts.xml**
```xml
<action name="login" class="com.example.LoginAction">
    <result name="success">/WEB-INF/home.jsp</result>
    <result name="input">/WEB-INF/login.jsp</result>
</action>
```

**LoginAction.java**
```java
public class LoginAction extends ActionSupport {
    private String username;   // populated from request params via setters
    private String password;

    @Override
    public String execute() {
        if (authService.check(username, password)) return SUCCESS;
        addActionError("Bad credentials");
        return INPUT;
    }
    // getters/setters required — that's how binding works
}
```

### Config 
**Three layers**:
1. *Where configuration lives*, and which source wins when several set the same thing
	- `default.properties`
	- `struts-default.xml` 
	- plugins’ `struts-plugin.xml` 
	- your `struts.xml`
	- `struts.properties` 
	- `web.xml` init-params.
2. *Constants*: global framework settings, like Spring Boot’s `application.properties`.
	- e.g. `<constant name="struts.devMode" value="false"/>`
3. *Structural config*: packages, actions, results, and interceptors in `struts.xml` (or annotations).
	- **`<package>`** groups actions. `namespace` is the URL prefix, `extends` inherits settings (usually from `struts-default`), and `abstract="true"` makes it a template without actions.
	- **`<action>`** maps a URL to a class and method, plus its `<result>`s.
	- `<interceptors>` / `<default-interceptor-ref>` define stacks and choose the default one.
	- `<global-results>` / `<global-exception-mappings>` are shared results and error handling.
	- **`<include>`** splits configuration into several files.

**ALSO**, Convention Plugin lets as replace some of the xml config with annotations like `@Action`, `@Result`, etc. 