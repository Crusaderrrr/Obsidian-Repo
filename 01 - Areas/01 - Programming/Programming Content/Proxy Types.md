**Dynamic Proxy**
![[Pasted image 20261104125218.png]]
- it is interface based 
- `ContactServiceImpl` has a method with `@Transactional` annotation
- When the method is invoked Dynamic Proxy creates a new class that implements the interface that is implemented by a target class 
	- that proxy is just a transaction logic, it has no business logic at all 
- then calls `InvocationHandler.invoke(proxy, method, args)` with the chain of transaction interceptors
- in the end it calls the original method via reflection

**CGLib Proxy** (the one used in spring boot by default)
![[Pasted image 20261104133247.png]]
- The only difference from Dynamic Proxy is that this one creates a class that extends the target class, **it does not give a fuck if there is or there isn't an interface**.
- At startup it creates a class directly as bytecode
- The created class is loaded directly to JVM, it does not need a source file
- Every overridable method (non-`final`, non-`private`, non-`static`) is overridden:
```java
class OrderService$$SpringCGLIB$$0 extends OrderService {
    private MethodInterceptor callback;   // Spring's DynamicAdvisedInterceptor

    @Override
    public void placeOrder(Order o) {
        // no business logic here
        callback.intercept(this, placeOrderMethod, new Object[]{o}, placeOrderMethodProxy);
    }
}
```
- Same shit here, it runs interceptor and in the end of that chain the target method is called
- all fields of the proxy are null, because it is created without calling a constructor

|                                    | **JDK dynamic proxy**      | **CGLIB proxy**                            |
| ---------------------------------- | -------------------------- | ------------------------------------------ |
| *How the proxy gets your type*     | Implements your interfaces | Subclasses your class                      |
| *Injectable as the concrete class* | No                         | Yes                                        |
| *Methods that can be intercepted*  | Interface methods only     | Non-final, non-private, non-static methods |
| *Requirements*                     | At least one interface     | Class not `final`                          |
| *Default in Spring Boot*           | No                         | Yes, since 2.0                             |
| *Calls your code on*               | Separate target            | Separate target                            |
| *Self-invocation intercepted*      | No                         | No                                         |
