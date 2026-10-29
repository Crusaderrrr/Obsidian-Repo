> [!info] How to use
> - `[x]` only when I can explain it **without notes** ([[Active recall]], [[Метод Феймана]]) and have used it in code.
> - `— [[Note]]` = I already have a note → re-read, close it, explain out loud, then check.
> - Main practice project: [[GHA plan]] — most new items below come from its stages.

## TypeScript / JavaScript

### Базовый фундамент TS/JS
- [ ] Понимаю разницу между `let`, `const`, `var` — [[Переменные]]
- [ ] Хорошо понимаю область видимости и замыкания — [[Scopes]], [[Closure]]
- [ ] Понимаю, как работает `this` в разных контекстах — [[This]]
- [ ] Понимаю, как работает event loop, microtasks и macrotasks — [[Event Loop]]
- [ ] Уверенно использую `async/await`, знаю, как это связано с промисами — [[Await]], [[Promises]]

### Типизация в TypeScript
- [ ] Уверенно использую интерфейсы и типы (`interface`, `type`) — [[Types]]
- [ ] Понимаю разницу между `interface` и `type`
- [ ] Умею описывать типы для функций (параметры, возвращаемые значения)
- [ ] Использую union и intersection типы (`|` и `&`) — [[Types]], [[Type Narrowing]]
- [ ] Понимаю, как работают generics в функциях и интерфейсах — [[Generics ts]]
- [ ] Умею типизировать асинхронный код (промисы, API‑вызовы)
- [ ] Использую utility types (`Partial`, `Pick`, `Omit`, `Required`, `Readonly`)
- [ ] Умею выводить типы из существующих значений (`typeof`, `keyof`)
- [ ] Conditional types и `infer` — [[Conditional Types]]
- [ ] Discriminated unions + exhaustive check через `never` — [[Types]]

### Архитектура фронта (на уровне языка)
- [ ] Умею разделять код на модули (import/export) — [[Модули]]
- [ ] Не использую `any` без крайней необходимости (`unknown` вместо него)
- [ ] Умею вынести общие типы в отдельный модуль
- [ ] Могу описать типизацию для API‑слоя (dto/response типы)
- [ ] Валидирую ответы API в рантайме (zod) — типы TS исчезают после компиляции

### React (for [[GHA plan]] stage 8)
- [ ] Components, props, state — [[Component]], [[Props]], [[State]]
- [ ] `useEffect` rules: dependencies, cleanup, why it double-runs in StrictMode — [[Hooks]]
- [ ] Data fetching with loading/error states (TanStack Query or plain fetch)
- [ ] Routing — [[Routing]]
- [ ] Charts for trend data (one library, e.g. Recharts)

---

## PostgreSQL

### SQL‑база
- [x] Уверенно пишу `SELECT`, `INSERT`, `UPDATE`, `DELETE`
- [x] Понимаю разницу между `INNER`, `LEFT`, `RIGHT`, `FULL` JOIN
- [x] Умею использовать агрегатные функции (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)
- [x] Знаю, как работают `GROUP BY` и `HAVING`
- [x] Понимаю, когда использовать подзапросы

### Продвинутый SQL
- [ ] Умею использовать оконные функции (`ROW_NUMBER`, `RANK`, `OVER (PARTITION BY ...)`)
- [x] Понимаю разницу между `EXISTS` и `IN`
- [ ] Могу переписать сложный запрос на несколько более простых (CTE, `WITH`)
- [ ] `INSERT ... ON CONFLICT` (upsert) — нужно для идемпотентного импорта в [[GHA plan]]
- [ ] Bulk insert: `COPY` / batch insert vs построчный insert

### Индексы и производительность
- [ ] Понимаю, как работают B‑tree индексы в PostgreSQL
- [ ] Умею создавать и удалять индексы (`CREATE INDEX`, `DROP INDEX`, `CONCURRENTLY`)
- [ ] Знаю, когда индекс помогает, а когда мешает
- [ ] Составные, частичные и covering индексы (`INCLUDE`), порядок колонок
- [ ] Умею читать план выполнения запроса (`EXPLAIN`, `EXPLAIN (ANALYZE, BUFFERS)`)
- [ ] Понимаю разницу между sequential scan, index scan, bitmap scan
- [ ] Нахожу медленные запросы через `pg_stat_statements`

### Транзакции и изоляция
- [x] Понимаю, что такое ACID — [[ACID]]
- [x] Знаю базовые уровни изоляции транзакций — [[How transactions work]]
- [x] Понимаю, что такое dirty read, non‑repeatable read, phantom read
- [ ] Optimistic vs pessimistic locking, `SELECT ... FOR UPDATE` — [[Optimistic and Pessimistic locking]]
- [ ] Очередь задач на Postgres: `FOR UPDATE SKIP LOCKED` ([[GHA plan]] stage 7)
- [ ] MVCC и VACUUM на базовом уровне (почему `DELETE` не освобождает место)

### Дизайн схемы и миграции
- [ ] Понимаю нормализацию (1NF, 2NF, 3NF) на базовом уровне
- [ ] Могу спроектировать несколько связанных таблиц под конкретный бизнес‑кейс
- [ ] Декларативное партиционирование по времени, удаление старых партиций ([[GHA plan]] stage 2–3)
- [ ] Flyway: versioned migrations, почему нельзя редактировать применённую миграцию
- [ ] Знаю паттерны безопасных миграций (expand‑and‑contract)
- [ ] Могу написать миграцию, которая не ломает прод (без долгих блокировок)
- [ ] Понимаю, как проверять миграции на тестовом окружении до продакшена

---

## Spring (Core, MVC, Data)

### Core Spring / контейнер
- [x] Понимаю идею IoC и Dependency Injection — [[Inversion of Control]], [[Spring Dependency Injection]]
- [x] Знаю, как поднимается ApplicationContext — [[ApplicationContext]], [[How Spring works]]
- [ ] Умею использовать `@Configuration` и `@Bean` — [[Spring Bean]]
- [x] Понимаю разницу между component‑сканированием и явной декларацией бинов
- [x] Знаю основные scope’ы бинов (singleton, prototype и т.п.)
- [ ] Constructor injection vs `@Autowired` на поле — почему constructor лучше
- [ ] `@ConfigurationProperties` вместо россыпи `@Value` — [[@Value]], [[Spring Profiles]]
- [ ] Как работают прокси (JDK vs CGLIB) и почему `@Transactional` не срабатывает при self‑invocation

### Spring MVC / Web
- [ ] Уверенно пишу контроллеры (`@Controller`, `@RestController`) — [[Controllers]]
- [x] Понимаю, как работает маппинг запросов (`@RequestMapping`, `@GetMapping`, ...) — [[Spring MVC]], [[Dispatcher Servlet]]
- [ ] Умею работать с path variables, query params, request body
- [ ] Знаю, как глобально обрабатывать ошибки (ControllerAdvice, exception handlers, `ProblemDetail`)
- [ ] Понимаю, как устроены фильтры и интерцепторы в Spring — [[Spring Filters & Interceptors]]
- [ ] Пагинация (`Pageable`) и почему offset медленный на больших таблицах (keyset)

### Spring Data / JPA
- [x] Понимаю, как маппятся сущности на таблицы (`@Entity`, `@Table`, `@Column`) — [[Java Persistence API]]
- [x] Умею описывать связи (`@OneToMany`, `@ManyToOne`, `@ManyToMany`, `@OneToOne`)
- [x] Понимаю разницу между LAZY и EAGER загрузкой
- [x] Знаю, что такое N+1 проблема и как её избегать — [[N+1 Problem]]
- [ ] Умею писать репозитории (CRUD, кастомные запросы) — [[Spring Data JPA]], [[Criteria API]]
- [ ] Понимаю, как работают транзакции в Spring (`@Transactional`: propagation, rollback rules, readOnly)
- [ ] Знаю, когда JPA лишний и лучше `JdbcClient` / `JdbcTemplate` (bulk import в [[GHA plan]])
- [ ] Persistence context, dirty checking, `LazyInitializationException` — [[Hibernate]]

### Spring Security
- [ ] Security filter chain: где он стоит относительно DispatcherServlet — [[Spring Security]], [[Spring Filters & Interceptors]]
- [ ] Хранение паролей — [[BCryptPasswordEncoder]], [[UserDetailsService]]
- [ ] JWT: access + refresh flow — [[JWT Authentication]], [[Refresh JWT]]
- [ ] Refresh token rotation + хранение хэша токена в БД, а не самого токена
- [ ] CSRF: когда нужен, когда нет (cookie vs header auth) — [[CSRF Token]]
- [ ] Method security (`@PreAuthorize`) и тест «каждая роль видит только своё»

### Валидация и DTO
- [x] Использую Bean Validation (`@NotNull`, `@Size`, и др.)
- [x] Умею разделять entity и DTO
- [x] Умею маппить entity ↔ DTO (вручную или через MapStruct/аналог)

### Тестирование в Spring
- [x] Умею писать unit‑тесты для сервисов (с моками зависимостей)
- [x] Знаю, как писать интеграционные тесты с поднятием контекста
- [x] Могу протестировать репозиторий на реальной/embedded БД
- [ ] Testcontainers + `@ServiceConnection` (Postgres в тестах как в проде)
- [ ] Test slices: `@WebMvcTest`, `@DataJpaTest` — когда не нужен весь контекст
- [ ] Мок внешних HTTP API (WireMock / MockRestServiceServer), таймауты и 5xx

### Resilience & HTTP clients ([[GHA plan]] stage 7)
- [ ] `RestClient` (Spring 6+) вместо `RestTemplate`
- [ ] Retries с backoff, rate limit, circuit breaker — Resilience4j
- [ ] Идемпотентность: повторный запуск задачи не создаёт дублей

---

## Docker

### Базовые концепции
- [x] Понимаю разницу между образом (image) и контейнером (container) — [[Docker]], [[VM vs Docker Container]]
- [x] Знаю, как смотреть запущенные контейнеры, логи, статусы
- [x] Умею запускать контейнер с маппингом портов и томов

### Dockerfile
- [x] Умею писать простой Dockerfile для Java‑приложения
- [ ] Multi-stage build (JDK для сборки, JRE для запуска)
- [ ] Понимаю, что такое слои образа и кэширование
- [x] Использую `.dockerignore` для уменьшения размера образа
- [x] Знаю, как собрать образ и запушить его в registry

### Docker Compose
- [x] Умею описать несколько сервисов в `docker-compose.yml` (app + db)
- [x] Понимаю, как задать сети, переменные окружения, тома
- [x] `healthcheck` + `depends_on: condition: service_healthy`
- [ ] Могу локально поднять весь стек проекта через docker‑compose ([[GHA plan]] stage 1)

### Практические навыки
- [x] Локально разворачиваю PostgreSQL через Docker для разработки
- [ ] Умею дебажить проблемы с контейнерами (логи, порты, зависимости)
- [ ] Понимаю основы docker‑сетей (bridge, порты, алиасы)

---

## CI/CD & Deploy
- [ ] GitHub Actions: workflow, jobs, cache для Maven/Gradle — [[GitHub Actions]]
- [ ] Запуск Testcontainers-тестов в CI
- [ ] Сборка и пуш Docker-образа из CI
- [ ] Деплой на VPS: SSH-ключи, systemd или compose, reverse proxy (Caddy/Nginx) + HTTPS — [[SSH Protocol]], [[Linux Commands]]
- [ ] Секреты: env-переменные, не коммитить `.env`

## Observability ([[GHA plan]] stage 5)
- [ ] Structured logging (JSON), correlation id через MDC
- [ ] Spring Boot Actuator: health, metrics endpoints
- [ ] Micrometer: counter, timer, gauge — что когда использовать
- [ ] Prometheus scrape + Grafana dashboard
- [ ] Метрики HikariCP и JVM: что значит «пул исчерпан»

## Performance & Profiling ([[GHA plan]] stage 6)
- [ ] Load testing (Locust / k6), percentiles p50/p95/p99 вместо среднего
- [ ] JFR + JDK Mission Control
- [ ] async-profiler, flame graphs
- [ ] Журнал оптимизаций: гипотеза → изменение → цифры до/после

---

## Object-Oriented Programming
- [x] SOLID principles (Single Responsibility, Open/Closed, Liskov, Interface Segregation, Dependency Inversion) — [[SOLID]]
- [ ] Design patterns — Creational (Builder, Factory, Singleton, Prototype) — [[Builder Pattern]], [[Factory Pattern]], [[Abstract Factory Pattern]], [[Singleton Pattern]], [[Prototype Pattern]]
- [ ] Design patterns — Structural (Adapter, Decorator, Proxy, Composite) — [[Decorator Pattern]]
- [ ] Design patterns — Behavioral (Strategy, Observer, Command, Template Method, Iterator) — [[Strategy Pattern]], [[Observer Pattern]], [[Command Pattern]], [[Template Method Pattern]], [[CoR Pattern]]
- [ ] Где эти паттерны живут в Spring (Proxy → AOP/`@Transactional`, Template Method → `JdbcTemplate`, CoR → filter chain)
- [x] Composition over inheritance principle — [[Composition over inheritance principle]]
- [x] Abstract classes vs interfaces — when to use each — [[Questions Java]]
- [ ] Covariance and contravariance in type hierarchies

---
# Java
## Generics
- [ ] Generic classes and generic methods — [[Generics]]
- [ ] Bounded type parameters (`<T extends Comparable<T>>`)
- [ ] Wildcards — upper bounded (`<? extends T>`), lower bounded (`<? super T>`), unbounded (`<?>`) — PECS
- [ ] Type erasure — what it is and its practical implications
- [ ] Generic interfaces and their implementations

## Collections & Data Structures
- [ ] `equals()` and `hashCode()` contract — why they must be consistent
- [ ] `HashMap` internals — hashing, buckets, load factor, rehashing — [[Hash Table]], [[Коллизия]]
- [ ] `HashMap` vs `LinkedHashMap` vs `TreeMap` — when to use each — [[Collections]]
- [ ] `HashSet` vs `LinkedHashSet` vs `TreeSet`
- [ ] `ArrayList` vs `LinkedList` — performance tradeoffs — [[Массив и связанный список]]
- [ ] `ArrayDeque` as a stack/queue replacement
- [ ] `Collections` utility class — `unmodifiableList`, `synchronizedList`, `sort`, `binarySearch`
- [ ] `List.of()` vs `Collections.unmodifiableList()` vs `Arrays.asList()`
- [ ] `Comparable` vs `Comparator`

## Streams & Functional Programming
- [ ] Lambda expressions and functional interfaces (`Function`, `Predicate`, `Consumer`, `Supplier`, `BiFunction`) — [[Lambda Expressions]]
- [ ] Method references (`Class::method`, `instance::method`, `Class::new`) — [[Method Reference Operator]]
- [ ] Stream pipeline — source, intermediate operations, terminal operations — [[Streams]]
- [ ] `filter`, `map`, `flatMap`, `distinct`, `sorted`, `peek`
- [ ] `reduce`, `collect`, `count`, `findFirst`, `anyMatch`, `allMatch`
- [ ] `Collectors` — `toList`, `toMap`, `groupingBy`, `partitioningBy`, `joining`
- [ ] Parallel streams — when useful and when dangerous
- [ ] `Optional<T>` — proper usage and avoiding `.get()` without checking — [[Optional]]

## Exception Handling
- [x] Checked vs unchecked exceptions — design decisions — [[Exceptions]]
- [ ] Custom exception hierarchies
- [ ] `try-with-resources` and `AutoCloseable`
- [ ] Multi-catch blocks and exception chaining (`initCause`, `getCause`)
- [x] Best practices — never swallow exceptions, log properly, fail fast

## Concurrency & Multithreading
- [ ] `Thread` lifecycle and `Runnable` vs `Callable` — [[Threading]]
- [ ] `synchronized` keyword — method-level and block-level
- [ ] `volatile` keyword — visibility guarantee
- [ ] `java.util.concurrent` package overview — [[Concurrent Programming]], [[Multithreading]]
- [ ] `ExecutorService`, `ThreadPoolExecutor`, `ScheduledExecutorService`
- [ ] `Future<T>` and `CompletableFuture` — chaining with `thenApply`, `thenCompose`, `exceptionally`
- [ ] `ReentrantLock`, `ReadWriteLock`
- [ ] Concurrent collections — `ConcurrentHashMap`, `CopyOnWriteArrayList`, `BlockingQueue`
- [ ] Deadlocks — how they occur and how to prevent them
- [ ] `happens-before` relationship in the Java Memory Model
- [ ] Virtual threads (Java 21): when they help (I/O) and when not (CPU, pinning)
- [ ] `spring.threads.virtual.enabled=true` — what changes in a Spring Boot app

## JVM Internals
- [ ] JVM memory model — heap, stack, method area, metaspace — [[Memory]]
- [x] Garbage collection — how GC works, generational GC (Young/Old/PermGen) — [[Java Garbage Collector]]
- [x] GC algorithms overview — Serial, Parallel, G1, ZGC
- [ ] Class loading mechanism — Bootstrap, Platform (ex-Extension), Application classloaders — [[From source to running process]]
- [ ] `OutOfMemoryError` vs `StackOverflowError` — causes and debugging (heap dump)
- [ ] JIT compilation basics
- [ ] Container-aware JVM: `-XX:MaxRAMPercentage` in Docker

## Modern Java (17–25)
- [ ] `var` keyword (local type inference, Java 10+)
- [ ] Text blocks (Java 15+)
- [ ] Records (Java 16+) — as DTOs
- [ ] Sealed classes and interfaces
- [ ] Pattern matching for `instanceof` and `switch` (Java 21)
- [ ] Record patterns (Java 21)
- [ ] Sequenced collections — `getFirst()`, `getLast()`, `reversed()` (Java 21)
- [ ] Scoped values, structured concurrency (Java 25)
- [ ] Spring Boot 4 / Spring Framework 7: что изменилось (null-safety with JSpecify, API versioning)

---

## Notes to write / fix
Empty or stub notes worth finishing (writing them = best self-test):
- [ ] [[Abstract Class vs Interface]] — empty; content already sits in [[Questions Java]], move it here
- [ ] [[Detecting errors using Git]] — empty (`git bisect`)
- [ ] [[HTTPS]], [[DOM]], [[Protocols]], [[Hash Function]] — one-liners
- [ ] [[TypeScript]] — turn into a MoC for the TS content notes
- [ ] Delete duplicates: `TCP-IP model(1)` (empty), `Concurrent Programming(1)`, `Optimistic and Pessimistic locking(1)`, `Linux Structure(1)`, `Framework(1)`

New notes that match the roadmap:
- [ ] Indexes & EXPLAIN
- [ ] Window functions
- [ ] `@Transactional` deep dive
- [ ] `equals` / `hashCode` + HashMap internals
- [ ] CompletableFuture & Virtual threads
- [ ] Testcontainers
- [ ] Flyway
- [ ] Observability (Micrometer → Prometheus → Grafana)
