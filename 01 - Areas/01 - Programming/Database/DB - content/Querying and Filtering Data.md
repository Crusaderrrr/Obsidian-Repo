---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - database
  - postgres
note type: Informational Note
---
## Select
```sql
SELECT column1, column2, ...  
FROM table_name  
WHERE condition;
```

*Example*:
```sql
SELECT * FROM employees WHERE department = 'IT';
```

## Select Distinct clause
Prevents fetching duplicates.
```sql
SELECT DISTINCT column_1 FROM table_name;
```

*Example*:
```sql
SELECT  
    DISTINCT colour_1  
FROM  
    my_table  
ORDER BY  
    colour_1;
```