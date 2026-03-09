Those are simply **named, stored block of SQL code that accepts input and returns a result**.
They are stored in the db directly and can be used from anywhere (any query).

The simple *example*:
```sql
CREATE OR REPLACE FUNCTION get_full_name(first_name TEXT, last_name TEXT)
RETURNS TEXT
LANGUAGE sql
AS $$
    SELECT first_name || ' ' || last_name;
$$;

-- calling it
SELECT get_full_name('Nikita', 'Doe'); -- returns "Nikita Doe"

```

The functions can be written in 4 languages, not only SQL:
- `sql`
- `plpgsql` - procedural logic: loops, conditionals, variables
- `plpython` - Python logic inside DB
- `plv8` - JS inside DB

Also since Postgres 11 there are **Procedures**, which *can commit/rollback transactions* (functions cannot).