---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
In Spring framework we have many ways of querying database, the main three of them are:
- **JDBC API** - which is Java *Database Connectivity*, this is used to make a raw db SQL queries.
- **JdbcTemplate** - small wrapper around JDBC API. Part of Spring Framework. Offers some abstractions.
- **JPA** - *Java Persistent API*, which is a Java standard specification for ORM. Set of rules and interfaces.
	- **Hibernate** - It is ORM (Object Relational Mapping), this thing provides the highest level of abstraction. Implementation of *JPA*.
	- **Spring Data JPA** - is a high-level abstraction built on top of JPA and ORM frameworks like Hibernate.
---
# DataSource

This is **core bean** that acts as a factory for database connections. It abstracts and manages the details of connecting to a specific database, providing connections for executing SQL queries and transactions.
- **Purpose:** It represents a pool of database connections. Instead of opening and closing a new connection each time, it *reuses connections*, improving performance and resource management.
	- **Configuration**: it is autoconfigured with data from `application.properties` or `application.yml`

---
# JDBC API
### JDBC Connection 
- we need a dependency of `JDBC driver postgreSQL`
- after that in our DAO model, where all the queries should be located, create a connection with our db
- In DAO methods we make queries 

### PreparedStatement
This is kind of statement that prevents *SQL injection*, and makes queries to database faster, because this query is compiled only once (when created), but simple Statement query is compiled every time we make a query. Also this PS can be cached in db.

An example method in DAO:
```java
  public void save(Person person) {
    try {

      PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO Person VALUES (1, ?, ?, ?)");
      preparedStatement.setString(1, person.getName());
      preparedStatement.setInt(2, person.getAge());
      preparedStatement.setString(3, person.getEmail());
  

      preparedStatement.executeUpdate();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }
```
1. Create a PreparedStatement instance with a blueprint for the query
2. Set PS parameters
3. Execute PS


# JDBC Template
As told before, this is some kind of wrapper over JDBC API that offers some abstraction. 

In JDBC API we have many problems:
- Duplication of the code
- Very low level of abstraction
- SQLException which has no relative info and needed to be implemented everywhere

Using JDCB Template we can get from writing 20 lines of code to 1 line.

**First step**:
we need to set up:
```java
    @Bean
    public DataSource dataSource() {
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName("org.postgresql.Driver");
        dataSource.setUrl("jdbc:postgresql://localhost:5432/Java_DB");
        dataSource.setUsername("postgres");
        dataSource.setPassword("2124648306fF");
        return dataSource;
    }

    @Bean
    public JdbcTemplate jdbcTemplate() {
        return new JdbcTemplate(dataSource());
    }
```
- first bean is the source of the data (connection to the db)
- second bean is connection of the JdbcTemplate to this source 

**Second**:
when implementing DAO logic, we need to firstly create a Mapper class that will implement a *RowMapper* interface to enable some features.

If properties of our class are the same as fields of the table in database -> we can use *BeanPropertyRowMapper* which is already implemented for us.

