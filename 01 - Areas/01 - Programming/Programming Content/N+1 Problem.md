This is a **database query problem** when TOO MANY requests are made for a single operation.

**Example**:
```java
// 1 query: SELECT * FROM users
List<User> users = userRepo.findAll();

for (User user : users) {
    // N queries: SELECT * FROM orders WHERE user_id = ?
    // Fires once per user — separately!
    List<Order> orders = user.getOrders();
}
```

**Example in words**:
If we have N records, then we end up with N+1 queries:
- 1 -> fetch the list of parents 
- N -> one extra query per parent to fetch its children
So 100 users = 101 queries instead of 1.

## How to fix
Use `JOIN FETCH` like that:
```java
// In your repository — fetches users AND their orders in one query
@Query("SELECT u FROM User u JOIN FETCH u.orders")
List<User> findAllWithOrders();
```