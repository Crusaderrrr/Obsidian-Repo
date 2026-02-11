---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
Spring Data JPA is a framework that *simplifies database access* in Spring-based applications by providing an abstraction layer over the **Java Persistence API** (JPA). Its purpose is to make it easier to integrate with relational databases using Object-Relational Mapping (ORM), allowing developers to work with database records as Java objects without writing boilerplate SQL queries.

What JPA does is explained [[Database|here]].

It supports **autocreation of tables** in Database, but this requires a JPA provider, such as [[Hibernate]]. 
- After adding `@Entity` annotation to a class Spring will recognize it as a table.
- The configuration of the autocreation lives in `application.properties` where we can specify the `spring.jpa.hibernate.ddl-auto` equal to update.

## @Table  Annotation

It is used to define some additional information:
- Define other table name to link `@Entity`
- Customize schemas, catalog, columns, etc.