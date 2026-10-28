**Filter** - a servlet-level component that wraps every request before [[Spring MVC]] even sees it.
**Interceptor** - a [[Spring MVC]] component that runs inside a `DispatcherServlet`.

**Execution order**:
Client
  → *Filter 1* (before)
    → *Filter 2* (before)            ← Spring Security lives here
      → *DispatcherServlet*
          → *Interceptor*.preHandle()        (return false = stop)
              → *Controller method*
          → *Interceptor*.postHandle()       (skipped if controller threw)
          → (view rendering, if any)
          → *Interceptor*.afterCompletion()  (runs if preHandle returned true)
    ← *Filter 2* (after)
  ← *Filter 1* (after)

A **filter** has a `doFilter` method, that can interact with the request and response.
An **Interceptor** offers three methods to override.

**Filter example**:
![[Pasted image 20261028143214.png]]

**Interceptor example**:
![[Pasted image 20261028143333.png]]