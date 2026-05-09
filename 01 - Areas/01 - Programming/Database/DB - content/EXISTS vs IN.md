**EXISTS** is for checking whether a subquery **returns at least one row**, while *IN* is for checking whether a *value matches any value in a list or subquery result*.

Main difference
- `EXISTS` answers: “Does a matching row exist?”
- `IN` answers: “Is this value in that set?”

The next two queries return the same, but the logic is different, which shows the difference between those keywords:

`EXISTS`:
```sql
SELECT *
FROM customers c
WHERE EXISTS (
  SELECT 1
  FROM orders o
  WHERE o.customer_id = c.id
);
```

`IN`:
```sql
SELECT *
FROM customers
WHERE id IN (
  SELECT customer_id
  FROM orders
);
```