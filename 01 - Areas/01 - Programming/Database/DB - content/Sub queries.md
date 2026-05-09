We can make queries inside other queries.

## Examples
```sql
-- Employees paid above average
SELECT *
FROM employees
WHERE salary > (
  SELECT AVG(salary)
  FROM employees
);
```

```sql
-- Customers who have at least one order
SELECT *
FROM customers c
WHERE EXISTS (
  SELECT 1
  FROM orders o
  WHERE o.customer_id = c.id
);
```


```sql
-- Products in a specific category list
SELECT *
FROM products
WHERE category_id IN (
  SELECT id
  FROM categories
  WHERE active = true
);
```

# When to Use 
- Along with aggregation functions (`AVG`, `MIN`, `COUNT`, etc.)
- To filter by membership, using `IN`, `ANY`, `ALL`, or `EXISTS`
- To pre-aggregate or reshape data before the outer query uses it