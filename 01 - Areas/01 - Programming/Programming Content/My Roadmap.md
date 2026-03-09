
## TypeScript / JavaScript

### Базовый фундамент TS/JS
- [x] Понимаю разницу между `let`, `const`, `var`
- [x] Хорошо понимаю область видимости и замыкания
- [x] Понимаю, как работает `this` в разных контекстах
- [x] Понимаю, как работает event loop, microtasks и macrotasks
- [x] Уверенно использую `async/await`, знаю, как это связано с промисами

### Типизация в TypeScript
- [x] Уверенно использую интерфейсы и типы (`interface`, `type`)
- [x] Понимаю разницу между `interface` и `type`
- [x] Умею описывать типы для функций (параметры, возвращаемые значения)
- [x] Использую union и intersection типы (`|` и `&`)
- [x] Понимаю, как работают generics в функциях и интерфейсах
- [ ] Умею типизировать асинхронный код (промисы, API‑вызовы)
- [ ] Использую utility types (`Partial`, `Pick`, `Omit`, `Required`, `Readonly`)
- [ ] Умею выводить типы из существующих значений (`typeof`, `keyof`)

### Архитектура фронта (на уровне языка)
- [ ] Умею разделять код на модули (import/export)
- [ ] Не использую `any` без крайней необходимости
- [ ] Умею вынести общие типы в отдельный модуль
- [ ] Могу описать типизацию для API‑слоя (dto/response типы)

---

## PostgreSQL

### SQL‑база
- [x] Уверенно пишу `SELECT`, `INSERT`, `UPDATE`, `DELETE`
- [ ] Понимаю разницу между `INNER`, `LEFT`, `RIGHT`, `FULL` JOIN
- [ ] Умею использовать агрегатные функции (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)
- [x] Знаю, как работают `GROUP BY` и `HAVING`
- [ ] Понимаю, когда использовать подзапросы

### Продвинутый SQL
- [ ] Умею использовать оконные функции (`ROW_NUMBER`, `RANK`, `OVER (PARTITION BY ...)`)
- [ ] Понимаю разницу между `EXISTS` и `IN`
- [ ] Могу переписать сложный запрос на несколько более простых

### Индексы и производительность
- [ ] Понимаю, как работают B‑tree индексы в PostgreSQL
- [ ] Умею создавать и удалять индексы (`CREATE INDEX`, `DROP INDEX`)
- [ ] Знаю, когда индекс помогает, а когда мешает
- [ ] Умею читать план выполнения запроса (`EXPLAIN`, `EXPLAIN ANALYZE`)
- [ ] Понимаю разницу между sequential scan, index scan, bitmap scan

### Транзакции и изоляция
- [ ] Понимаю, что такое ACID
- [ ] Знаю базовые уровни изоляции транзакций
- [ ] Понимаю, что такое dirty read, non‑repeatable read, phantom read

### Дизайн схемы и миграции
- [ ] Понимаю нормализацию (1NF, 2NF, 3NF) на базовом уровне
- [ ] Могу спроектировать несколько связанных таблиц под конкретный бизнес‑кейс
- [ ] Знаю паттерны безопасных миграций (expand‑and‑contract)
- [ ] Могу написать миграцию, которая не ломает прод (без долгих блокировок)
- [ ] Понимаю, как проверять миграции на тестовом окружении до продакшена

---

## Spring (Core, MVC, Data)

### Core Spring / контейнер
- [ ] Понимаю идею IoC и Dependency Injection
- [ ] Знаю, как поднимается ApplicationContext
- [ ] Умею использовать `@Configuration` и `@Bean`
- [ ] Понимаю разницу между component‑сканированием и явной декларацией бинов
- [ ] Знаю основные scope’ы бинов (singleton, prototype и т.п.)

### Spring MVC / Web
- [ ] Уверенно пишу контроллеры (`@Controller`, `@RestController`)
- [ ] Понимаю, как работает маппинг запросов (`@RequestMapping`, `@GetMapping`, ...)
- [ ] Умею работать с path variables, query params, request body
- [ ] Знаю, как глобально обрабатывать ошибки (ControllerAdvice, exception handlers)
- [ ] Понимаю, как устроены фильтры и интерцепторы в Spring

### Spring Data / JPA
- [ ] Понимаю, как маппятся сущности на таблицы (`@Entity`, `@Table`, `@Column`)
- [ ] Умею описывать связи (`@OneToMany`, `@ManyToOne`, `@ManyToMany`, `@OneToOne`)
- [ ] Понимаю разницу между LAZY и EAGER загрузкой
- [ ] Знаю, что такое N+1 проблема и как её избегать
- [ ] Умею писать репозитории (CRUD, кастомные запросы)
- [ ] Понимаю, как работают транзакции в Spring (`@Transactional`)

### Валидация и DTO
- [ ] Использую Bean Validation (`@NotNull`, `@Size`, и др.)
- [ ] Умею разделять entity и DTO
- [ ] Умею маппить entity ↔ DTO (вручную или через MapStruct/аналог)

### Тестирование в Spring
- [ ] Умею писать unit‑тесты для сервисов (с моками зависимостей)
- [ ] Знаю, как писать интеграционные тесты с поднятием контекста
- [ ] Могу протестировать репозиторий на реальной/embedded БД

---

## Docker

### Базовые концепции
- [ ] Понимаю разницу между образом (image) и контейнером (container)
- [ ] Знаю, как смотреть запущенные контейнеры, логи, статусы
- [ ] Умею запускать контейнер с маппингом портов и томов

### Dockerfile
- [ ] Умею писать простой Dockerfile для Java‑приложения
- [ ] Понимаю, что такое слои образа и кэширование
- [ ] Использую `.dockerignore` для уменьшения размера образа
- [ ] Знаю, как собрать образ и запушить его в registry

### Docker Compose
- [ ] Умею описать несколько сервисов в `docker-compose.yml` (app + db)
- [ ] Понимаю, как задать сети, переменные окружения, тома
- [ ] Могу локально поднять весь стек проекта через docker‑compose

### Практические навыки
- [ ] Локально разворачиваю PostgreSQL через Docker для разработки
- [ ] Умею дебажить проблемы с контейнерами (логи, порты, зависимости)
- [ ] Понимаю основы docker‑сетей (bridge, порты, алиасы)

---

## Object-Oriented Programming
- [ ] SOLID principles (Single Responsibility, Open/Closed, Liskov, Interface Segregation, Dependency Inversion)
- [ ] Design patterns — Creational (Builder, Factory, Singleton, Prototype)
- [ ] Design patterns — Structural (Adapter, Decorator, Proxy, Composite)
- [ ] Design patterns — Behavioral (Strategy, Observer, Command, Template Method, Iterator)
- [ ] Composition over inheritance principle
- [ ] Abstract classes vs interfaces — when to use each
- [ ] Covariance and contravariance in type hierarchies

---
# Java
## Generics
- [ ] Generic classes and generic methods
- [ ] Bounded type parameters (`<T extends Comparable<T>>`)
- [ ] Wildcards — upper bounded (`<? extends T>`), lower bounded (`<? super T>`), unbounded (`<?>`)
- [ ] Type erasure — what it is and its practical implications
- [ ] Generic interfaces and their implementations

## Collections & Data Structures
- [ ] `equals()` and `hashCode()` contract — why they must be consistent
- [ ] `HashMap` internals — hashing, buckets, load factor, rehashing
- [ ] `HashMap` vs `LinkedHashMap` vs `TreeMap` — when to use each
- [ ] `HashSet` vs `LinkedHashSet` vs `TreeSet`
- [ ] `ArrayList` vs `LinkedList` — performance tradeoffs
- [ ] `ArrayDeque` as a stack/queue replacement
- [ ] `Collections` utility class — `unmodifiableList`, `synchronizedList`, `sort`, `binarySearch`
- [ ] `Comparable` vs `Comparator`

## Streams & Functional Programming
- [ ] Lambda expressions and functional interfaces (`Function`, `Predicate`, `Consumer`, `Supplier`, `BiFunction`)
- [ ] Method references (`Class::method`, `instance::method`, `Class::new`)
- [ ] Stream pipeline — source, intermediate operations, terminal operations
- [ ] `filter`, `map`, `flatMap`, `distinct`, `sorted`, `peek`
- [ ] `reduce`, `collect`, `count`, `findFirst`, `anyMatch`, `allMatch`
- [ ] `Collectors` — `toList`, `toMap`, `groupingBy`, `partitioningBy`, `joining`
- [ ] Parallel streams — when useful and when dangerous
- [ ] `Optional<T>` — proper usage and avoiding `.get()` without checking

## Exception Handling
- [ ] Checked vs unchecked exceptions — design decisions
- [ ] Custom exception hierarchies
- [ ] `try-with-resources` and `AutoCloseable`
- [ ] Multi-catch blocks and exception chaining (`initCause`, `getCause`)
- [ ] Best practices — never swallow exceptions, log properly, fail fast

## Concurrency & Multithreading
- [ ] `Thread` lifecycle and `Runnable` vs `Callable`
- [ ] `synchronized` keyword — method-level and block-level
- [ ] `volatile` keyword — visibility guarantee
- [ ] `java.util.concurrent` package overview
- [ ] `ExecutorService`, `ThreadPoolExecutor`, `ScheduledExecutorService`
- [ ] `Future<T>` and `CompletableFuture` — chaining with `thenApply`, `thenCompose`, `exceptionally`
- [ ] `ReentrantLock`, `ReadWriteLock`
- [ ] Concurrent collections — `ConcurrentHashMap`, `CopyOnWriteArrayList`, `BlockingQueue`
- [ ] Deadlocks — how they occur and how to prevent them
- [ ] `happens-before` relationship in the Java Memory Model

## JVM Internals
- [ ] JVM memory model — heap, stack, method area, metaspace
- [ ] Garbage collection — how GC works, generational GC (Young/Old/PermGen)
- [ ] GC algorithms overview — Serial, Parallel, G1, ZGC
- [ ] Class loading mechanism — Bootstrap, Extension, Application classloaders
- [ ] `OutOfMemoryError` vs `StackOverflowError` — causes and debugging
- [ ] JIT compilation basics

## Modern Java (11–17)
- [ ] `var` keyword (local type inference, Java 10+)
- [ ] Text blocks (Java 15+)
- [ ] Records (Java 16+)
- [ ] Sealed classes and interfaces (Java](<# Java Core Advanced Checklist

