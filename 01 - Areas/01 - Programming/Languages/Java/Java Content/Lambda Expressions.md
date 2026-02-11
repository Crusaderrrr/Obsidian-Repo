---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
These are inline anonymous functions that simplifies the use of functional programing concepts in Java.

## Types

1. No parameters, no return value:
```java
() -> System.out.println("Hello, World!");
```

2. Single parameter, single expression:
```java
x -> x * x
```

3. Multiple parameters and block body:
```java
(a, b) -> {
    int sum = a + b;
    return sum;
}
```

## Use Cases:
- Implementing a functional interface inline, e.g., Runnable or Comparator.
- Simplifying event listeners.
- Using with collection methods like `forEach`, `map`, `filter`.