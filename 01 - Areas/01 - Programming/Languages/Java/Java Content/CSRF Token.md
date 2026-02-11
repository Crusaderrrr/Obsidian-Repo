---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
  - crypto
note type: Informational Note
---
CSRF (**Cross-Site Request Forgery**) token is a cryptographically secure token, generated on server side, used on *state-changing operations*. Is validating that the request is intentional and made by authenticated user, preventing unauthorized operations.

## Difference with JWT
- Structure
- *CSRF* - prevents attacks to a server, *JWT* -  authenticates and authorizes users
- *CSRF* - sent with state changing request, *JWT* - sent with requests to identify and authorize users
- JWT is stateless, no session dependency. CSRF is.