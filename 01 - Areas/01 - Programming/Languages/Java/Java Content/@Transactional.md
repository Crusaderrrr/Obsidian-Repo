---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
Annotation that makes some method transactional (wraps it into transaction). 
Transactions in Spring use [[AOP]].

**When is it triggered?**
- When we call an annotated method using a proxy (from other class)

There are two proxy types:
- JDK Dynamic Proxy (Interface based)
- CGLib Proxy (Class based)
- More info: [[Proxy Types]]

**Transactional adds interceptors into the call chain of the target method**.
- they wrap the target method and run something before and/or after the method finished
- by default there is only one interceptor `TransactionInterceptor`, which opens/joins a transaction and then commits it or rolls back
- [[What TransactionInterceptor does]]
E.g.
```java
public interface MethodInterceptor {
    Object invoke(MethodInvocation invocation) throws Throwable;
}
```
**How the chain moves forward** (in case of multiple interceptors):
Spring’s `ReflectiveMethodInvocation` holds the list of interceptors and an index. Simplified:
```java
public Object proceed() throws Throwable {
    if (currentIndex == interceptors.size() - 1) {
        return method.invoke(target, args);           // end of chain: your real method
    }
    MethodInterceptor next = interceptors.get(++currentIndex);
    return next.invoke(this);                         // that interceptor will call proceed() again
}
```

### Simple example of how Transactional works
![[Pasted image 20261104140256.png]]
- controller calls a service method
- if a service method has Transactional annotation the proxy is created 
- that proxy is called instead of a real service
- interceptor chain is called 
- after interceptors the target method is called 
- when method finishes:
	- normal return -> transaction is commited
	- thrown error -> rollback 