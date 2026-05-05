## Logical Types

1. **Inner JOIN**
match on *both* tables
```sql
SELECT ... FROM a INNER JOIN b ON a.id = b.a_id;
```

2. **Left (Outer) JOIN**
*all* rows from the *left* + matching from the right
```sql
SELECT ... FROM a LEFT JOIN b ON a.id = b.a_id;
```

3. **Right (Outer) JOIN**
*all* rows from the *right* + matching from left
```sql
SELECT ... FROM a RIGHT JOIN b ON a.id = b.a_id;
```

4. **Full (Outer) JOIN**
all rows from both fetched, `NULL` where no reference
```sql
SELECT ...
FROM a
FULL JOIN b ON a.id = b.a_id;
```

5. **Cross JOIN**
```sql
SELECT ... FROM a CROSS JOIN b;
```
No condition, every row of `a` combined with every row of `b`

6. **Natural JOIN** 
Automatically joins on *all columns with the same name in both tables*.
```sql
SELECT ...
FROM a
NATURAL JOIN b;            -- natural inner
SELECT ...
FROM a
NATURAL LEFT JOIN b;       -- natural left outer
```

7. **SELF JOIN** (pattern)
That is not a separate keyword, just a table joined to itself with an alias
```sql
SELECT c1.id, c1.name, c2.name AS manager_name
FROM employees c1
LEFT JOIN employees c2
  ON c1.manager_id = c2.id;
```

## Physical join methods

PostgreSQL can execute the _same logical join_ using different algorithms. You see these in `EXPLAIN` output:
1. **Nested Loop Join**
    - Conceptually: for each row in outer, scan inner for matches.
    - Good when one side is small or highly selective, or when indexes help lookups.
2. **Hash Join**
    - Build an in‑memory hash table from one side, then probe it with rows from the other.
    - Good for large joins on equality conditions, given enough memory.
3. **Merge Join**
    - Sort both inputs on join keys and walk them in order, merging matches.
    - Good when inputs are already sorted on the join key (e.g. due to indexes or ORDER BY), and for large datasets.

PostgreSQL’s planner picks the method based on table statistics, indexes, and query structure.