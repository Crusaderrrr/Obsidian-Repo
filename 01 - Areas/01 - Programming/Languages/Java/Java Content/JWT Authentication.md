---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
Firstly, what is **JWT**?
- *JSON Web Token*
- Used to *further operations after authenticating user*.
- Is a long string of *encoded information* that consists of:
	1. *Header* (algorithm used for encoding)
	2. *Payload* (encoded data)
	3. *Signature* (verifies if this is valid JWT, secret key encoded here)
- These are stored in browser's memory
- Can be stolen be someone and used, it will work the same way as if the owner was using it
	- If it really happens, there is a *black list for JWTs* on every server