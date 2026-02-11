---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
![[Pasted image 20250818172637.png]]

Okay, imagine that we are making a simple SQL query to our database, and inside this query we need to perform *multiple queries*. 
To achieve it, we use `@Transactional` annotation.

Spring understands that on the part of the DB, it is necessary to create a transaction, in order to make all these queries succeed.

**But**
We did not specify any logic for this transaction, and it is compulsory.

Spring understands it, and creates a proxy (generates a code):
![[Pasted image 20250818173532.png]]

**But why does this happen**?
- Because in this new class Spring adds some secret logic

**Secret logic**:
![[Pasted image 20250818173842.png]]

- Start Transaction
- Perform original actions
- End Transaction
- Save this new bean to ApplicationContext as proxy, *but* with name of the original action