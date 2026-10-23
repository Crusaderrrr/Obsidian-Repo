**SQLite is a fast, self-contained, serverless, and lightweight SQL database engine implemented as a C-language library**

### Keys:
- *Serverless* - does not require a separate database server or daemon to run
- *Single-file storage* - all the data is stored in single file, which is then parsed
- *Normal DB* - it has [[ACID]] transactions, SQL queries like in [[PostgreSQL]] and other db features like [[JOINs]]

### Common use cases 
- *Embedded software* - inside OS (IOS, Android, etc.), inside browsers (Chrome, Firefox, Safari)
- *Local app storage* - Used by mobile and desktop apps to save user settings, offline cache, and local data

### Key Limitations
- *Write Concurrency*: Only one write operation can happen at a time per database file (though multiple simultaneous reads are supported).
- *No Built-in Replication:* It is designed as a single-node database rather than a distributed cluster server.

