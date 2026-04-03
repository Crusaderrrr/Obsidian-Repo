General database rules:

1. **Atomicity**
	"*All or nothing*", meaning that if some operations are executed, all of them should be successfully finished or all of them should not be processed/should be rolled back if something happens.
	
	Example:
	- We want to transfer some money from user1 to user2
	- Money gets removed from user1
	- *But*, it does not get to user2 for some reason
	- That problem should not be happening and can be solved using <mark style="background:#9254de">Transactions</mark>
2. **Consistency** 
	"*All the types should stay consistent*"
	
	Example:
	- If a certain column has a specified e.g. `CHECK (value >= 0)` 
	- That column should consist ONLY of proper data 
3. **Isolation**
	"*Concurrent transactions execute as if they were sequential*", meaning that one transaction cannot see intermediate dirty state of another.
	
	There are some *levels of isolation*:

| Isolation Level  | Dirty Read  | Non-repeatable Read | Phantom Read |
| ---------------- | ----------- | ------------------- | ------------ |
| Read Uncommitted | ✅ possible  | ✅ possible          | ✅ possible   |
| Read Committed   | ❌ prevented | ✅ possible          | ✅ possible   |
| Repeatable Read  | ❌ prevented | ❌ prevented         | ✅ possible   |
| Serializable     | ❌ prevented | ❌ prevented         | ❌ prevented  |
	<mark style="background:#b1ffff">Dirty Read</mark> - read from transaction while in process (not committed)
	<mark style="background:#b1ffff">Non-repeatable Read</mark> - read the same row twice within the same transaction and get different values because another transaction modified it in between.
	<mark style="background:#b1ffff">Phantom Read</mark> - when you run the same query twice within the same transaction and get different rows because another transactions have inserted or deleted rows.
4. **Durability**
	"*Once a transaction is committed, it stays committed*" — even if the server crashes immediately after. This is achieved by writing to a transaction log (WAL in PostgreSQL) before confirming the commit.