---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - database
  - postgres
note type: Informational Note
---

# Common PostgreSQL Data Types

| **Category**    | **Data Type**      | **Description**                                                  | **Example Usage**                      |
| --------------- | ------------------ | ---------------------------------------------------------------- | -------------------------------------- |
| **Boolean**     | `boolean`          | Stores true, false, or null values.                              | `true`, `false`                        |
| **Character**   | `char(n)`          | Fixed-length string padded with spaces.                          | `'A'`, `'ABC'` (length = n)            |
|                 | `varchar(n)`       | Variable-length string with max length `n`.                      | `'Hello'`, `'Postgres'`                |
|                 | `text`             | Variable-length string with unlimited length.                    | `'Long description text...'`           |
| **Numeric**     | `smallint`         | 2-byte integer, range: -32768 to 32767.                          | `123`, `-100`                          |
|                 | `integer`          | 4-byte integer (default integer type).                           | `1000`, `-5000`                        |
|                 | `bigint`           | 8-byte integer for very large numbers.                           | `10000000000`                          |
|                 | `decimal(p,s)`     | Exact numeric with user-defined precision and scale.             | `123.45`, `-987.65`                    |
|                 | `numeric(p,s)`     | Same as decimal, for precise calculations.                       | `1234.5678`                            |
|                 | `real`             | 4-byte floating point, single precision.                         | `3.14`, `-0.001`                       |
|                 | `double precision` | 8-byte floating point, double precision.                         | `3.1415926535`                         |
|                 | `serial`           | Auto-incrementing 4-byte integer (often for primary keys).       | `1, 2, 3...`                           |
|                 | `bigserial`        | Auto-incrementing 8-byte integer.                                | `1000000001...`                        |
| **Date/Time**   | `date`             | Calendar date (year, month, day).                                | `2024-08-10`                           |
|                 | `time`             | Time of day (hour, minute, second).                              | `14:30:00`                             |
|                 | `timestamp`        | Date and time without timezone.                                  | `2024-08-10 14:30:00`                  |
|                 | `timestamptz`      | Date and time with timezone info.                                | `2024-08-10 14:30:00-05`               |
|                 | `interval`         | Time span (days, hours, minutes, etc.).                          | `1 day`, `2 hours 30 mins`             |
| **UUID**        | `uuid`             | Stores Universally Unique Identifiers.                           | `550e8400-e29b-41d4-a716-446655440000` |
| **JSON**        | `json`, `jsonb`    | Storage of JSON data (`jsonb` is binary and indexable).          | `{"key": "value"}`                     |
| **Enum**        | `enum`             | User-defined set of static ordered values.                       | `'low', 'medium', 'high'`              |
| **Geometrical** | `point`            | A geometric point (x, y).                                        | `(1.0, 2.0)`                           |
|                 | `line`             | Infinite line.                                                   | `{1, -1, 0}`                           |
|                 | `lseg`             | Line segment.                                                    | `[(1,2),(3,4)]`                        |
|                 | `box`              | Rectangular box.                                                 | `((1,2),(3,4))`                        |
|                 | `path`             | Geometric path (open or closed).                                 | `[(0,0),(1,0),(1,1)]`                  |
|                 | `polygon`          | Polygon defined by multiple points.                              | `((0,0),(1,0),(1,1),(0,1))`            |
|                 | `circle`           | Circle with center point and radius.                             | `<(0,0),5>`                            |
| **Binary**      | `bytea`            | Variable-length binary data ("byte array").                      | `\xDEADBEEF`                           |
| **Array**       | `array`            | An array data type which offers a storage for multiple instances | `{1,2,3}`, could also be strings       |
