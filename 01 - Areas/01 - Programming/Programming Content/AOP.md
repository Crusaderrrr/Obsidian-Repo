AOP lets you write code like “log every method call” **once**, and Spring automatically runs it around many methods. You don’t paste the same lines into each method.

#### The problem
*Say you want to print a message whenever any service method runs*. Without AOP:
```java
public void createUser() {
    System.out.println("Method started");
    // create the user
    System.out.println("Method finished");
}

public void deleteUser() {
    System.out.println("Method started");
    // delete the user
    System.out.println("Method finished");
}

// ...and the same two lines in 200 more methods
```

That’s annoying, easy to forget, and it buries the real code.

#### With AOP
You write the printing code **once**:
```java
@Aspect
@Component
public class LoggingAspect {

    @Around("execution(* com.app.service.*.*(..))")   // WHERE: every method in the service package
    public Object log(ProceedingJoinPoint method) throws Throwable {
        System.out.println("Method started");          // WHAT: before
        Object result = method.proceed();              // run the real method
        System.out.println("Method finished");         // WHAT: after
        return result;
    }
}
```

Your methods become clean:
```java
public void createUser() {
    // create the user
}
```

When `createUser()` is called, the output is:
```
Method started
...user gets created...
Method finished
```