#### What `TransactionInterceptor` does
Take this method:
```java
@Transactional
public void placeOrder(Order o) {
    orderRepo.save(o);
    stockRepo.decrement(o.getItemId());
}
```

When `proxy.placeOrder(o)` is called, `TransactionInterceptor.invoke()` does the following:

**Before `proceed()`:**
1. **Reads the settings** from the annotation: propagation `REQUIRED`, default isolation, `readOnly=false`, rollback rules.
2. **Picks the transaction manager.** In your stack that’s `JpaTransactionManager`.
3. **Begins or joins a transaction:**
    - It checks the thread’s `ThreadLocal` for an active transaction.
    - If there is none: it opens an `EntityManager`, takes a JDBC connection from the pool, calls `connection.setAutoCommit(false)` (from now on the database won’t commit each statement on its own), and stores the EntityManager and connection in the `ThreadLocal`.
    - If there is one, `REQUIRED` just joins it, and nothing new is opened.

**`proceed()`:** your method runs. `orderRepo.save()` and `stockRepo.decrement()` both find the same EntityManager and connection in the `ThreadLocal`, so both statements go into one database transaction.

**After `proceed()`:**  
4. **Normal return:** commit. Hibernate flushes (sends the pending INSERT/UPDATE statements), then `connection.commit()` runs.  
5. **Exception thrown:** it checks the rollback rule. For a `RuntimeException` or `Error` it calls `connection.rollback()`. For a checked exception it **commits**, unless `rollbackFor` says otherwise. Then it rethrows the exception.  
6. **Cleanup:** it removes everything from the `ThreadLocal`, closes the EntityManager, returns the connection to the pool, and fires after-commit callbacks such as `@TransactionalEventListener`.