It enables **runtime query construction based on conditions**, it is safe and handles error for us.

## Components
- `CriteriaBuilder` -> factory from `EntityManager` *for creating* predicates, expressions, orderings, and queries.
- `CriteriaQuery<T>` -> Defines the *query root* (`SELECT`, `FROM`, `WHERE`);
	e.g. `cb.createQuery(Entity.class)`
- `Root<T>` -> represents the entity in `FROM` clause.
- **Predicate** -> `WHERE` conditions built with `cb.equal()`, `cb.like()`, `cb.and()/or()`, etc.
- `TypedQuery<T>` -> Executes via `em.createQuery(cq)` for type-safe results
- Supports joins `root.join("orders)`

## Example
```java
CriteriaBuilder cb = em.getCriteriaBuilder();
CriteriaQuery<Employee> cq = cb.createQuery(Employee.class);
Root<Employee> root = cq.from(Employee.class);
cq.select(root).where(cb.equal(root.get("dept"), "IT"));
List<Employee> results = em.createQuery(cq).getResultList();
```