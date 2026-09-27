Stands for **Language Server Protocol**

- this is a server that understands the concrete language, e.g. Java
- when an agent works with code it uses grep/regex to search, which is non-deterministic and token-heavy
- LSP server fixes that issue:

```text
AI writes/edits code
       ↓
Language Server checks it (compiles? types correct? references valid?)
       ↓
Errors sent back to AI
       ↓
AI fixes → repeat until clean
```
