#java #programming 

This is a **standard Java specification** (part of [[Platforms|Jakarta EE]]) **for Object-Relational Mapping** (ORM) that maps Java objects (entities) to relational database tables, handling CRUD operations without raw SQL.

*Core concepts*:
- `@Entity` annotations
- `EntityManager` that is used for managing (`fetch()`, `remove()`, `merge()`, etc.)
- Also used with config of datasource, etc.

*Typical flow*:
`EntityManagerFactory` -> get `EntityManager` -> perform transactions

---

Also used in spring: [[Spring Data JPA]]

There is also an interface called [[Criteria API]] in JPA.

