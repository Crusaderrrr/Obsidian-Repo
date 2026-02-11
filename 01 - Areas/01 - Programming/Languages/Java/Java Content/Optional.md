---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
- It acts as a wrapper around a value that may or may not be present.
    
- Instead of checking for `null`, you work with `Optional` methods to safely handle the presence or absence of a value.
    
- It provides various utility methods like:
    - `isPresent()` — checks if the value exists.
    - `get()` — retrieves the value if present, throws an exception otherwise.
    - `orElse(defaultValue)` — returns the actual value or a default if empty.
    - `orElseGet(Supplier)` — returns the value or computes a default via a supplier function.
    - `orElseThrow()` — throws an exception if the value is absent.
        
- You create `Optional` instances by:
    - `Optional.of(value)` — wraps a non-null value, throws if null.
    - `Optional.ofNullable(value)` — wraps a value that may be `null`.
    - `Optional.empty()` — represents an empty Optional.

## Example usage:
```java
Optional<String> name = Optional.ofNullable(getName());
String displayName = name.orElse("Unknown");
```