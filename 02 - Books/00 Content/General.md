This is what is told in first 8 chapters of the book:

#### Intro
- **Code read far more then written** (optimize for the reader, not writer)
- Think of yourself as an **author writing for an audience**, not just a programmer solving a problem
- **Leave code a little cleaner then you found it**
---
- [[Naming Conventions]]
---
#### Functions
- **Should be small**
- **do one thing only** 
- **Minimize arguments** (0 -> ideal, more -> meh...)
---
#### Comments
- **Good code doesn't need comments**
- Comments can lie, even javadoc
- There are bad and good comments (logically distinguished)
---
#### Formatting 
- Formatting is about **communication**
- **Vertical openness**: blank lines between concepts, dense lines for related things
- Related code should be **vertically close** (no scroll up, then down, then up another time)
---
#### Objects and data structures
- **Objects hide their data** behind abstractions and expose behavior [[OOP]]
- **Law of Demeter**: a method should only talk to its direct friends, not strangers (no long chains like `a.getB().getC().doSomething()`)

| #       | *data structure* | *object*  |
| ------- | ---------------- | --------- |
| exposes | raw data         behavior r  |

---
#### Error Handling
- **Don't return null**
- **Don't pass null** as arguments either - ends up in `NullPointerException`
- Error handling should be **separate from business logic**
---
#### Boundaries
- When using **third-party libraries**, wrap them in your own interface so your code doesn't depend directly on them
- Write **boundary tests** - helps to find errors, that are caused by API logic changes
---
#### Unit Tests
- They are **very important**
- Treat them as important as the actual code
- One concept for one test
- The **F.I.R.S.T** rules for good tests:
    - **F**ast — tests must run quickly or developers will stop running them
    - **I**ndependent — tests must not depend on each other, any test can run in any order
    - **R**epeatable — must work in any environment (local, CI, prod)
    - **S**elf-validating — must return a clear boolean pass/fail, not require manual log reading
    - **T**imely — write tests _before_ production code, not after



# Refactoring is your friend!
