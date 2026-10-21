**Universally Unique Identifier** is a 128-bit value that is *practically guaranteed to be unique* without any central authority handing out numbers

Example:
`550e8400-e29b-41d4-a716-446655440000`

It’s 32 hex characters in an 8-4-4-4-12 layout. The first digit of the third group is the **version** (here it’s `4`).

**Why use it over** `BIGSERIAL`:
- You can generate IDs anywhere (client, service, offline) before touching the DB, which helps with distributed systems and merging data.
- IDs aren’t guessable or enumerable. With sequential IDs, `/users/1235` invites someone to try 1236.