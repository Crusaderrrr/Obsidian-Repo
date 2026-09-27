This is a **waiter in the restaurant** (web server), which handles requests of clients, seating, connections, and routing. It receives the request, talks to database, applies some logic and returns the response. *Basically a controller*. 

In java we can create a servlet by extending the `javax.servlet.Servlet` or `HttpServlet` interface. It allows us to override two methods:
- `doPost()`
- `doGet()`

Example:
```java
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse res)
            throws IOException {
        res.setContentType("text/plain");
        res.getWriter().write("Hello, world");
    }
}
```