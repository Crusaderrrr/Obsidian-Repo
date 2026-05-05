It is a main container of the [[Inversion of Control]].

**Purpose**:
- instantiating 
- wiring 
- managing 
... lifecycle of all the application beans. All the beans are instantiated on application startup.

## Spring boot vs Spring 
The concept is the same, in boot it is more automatic.

## Startup

After `SpringApplication.run(MyApp.class, args)`:
- **Determine context type** - selects the concrete implementation of the dependency 
- **Create the context instance** - instantiates that implementation
- **Load configuration** - `@Configuration` classes, `application.properties`/`application.yml` and active `@Profile`s are resolved.
- **Component scan** - `@Component`, `@Service`, `@Repository`, `@Controller`, etc. are discovered and registered as bean definitions
- **Auto-configuration** - loads autoconfig classes (Tomcat, JPA, etc.)
- **Bean instantiation & DI** - all singleton beans are eagerly created and dependencies are injected
- **Embedded server start** - starts the embedded server, like Tomcat and registers a `DispatcherServlet`
- **Context refresh** - `ContextRefreshedEvent` is fired; `SmartLifecycle` beans (schedulers, Kafka listeners, etc.) are started
- **Post-startup** -  `CommandLineRunner` / `ApplicationRunner` beans execute; Actuator endpoints initialize