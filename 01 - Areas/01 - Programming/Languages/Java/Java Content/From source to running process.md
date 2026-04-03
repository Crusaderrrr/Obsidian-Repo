Explains the process **from plain java code to running application** (locally or deployed) also explains the difference between running *spring boot vs spring framework*.

# Steps of deploy process

1. **Maven/Gradle build**
	All the `.java` files are compiled to `.class` files (bytecode) by `javac` (compiler). 
	*Spring Boot*:
		Then mvn or gradle packages all those files into a Fat `JAR` file, that contains: compiled classes, dependency jars (Jackson, Spring, etc.), embedded Tomcat server, custom launcher.
	*Spring Framework*:
		Does the same thing, but the Tomcat is not embedded, and also the file could be `WAR`. So, external server is needed to deploy that jar.
2. **JVM**
	1. java launcher starts *new JVM process*
	2. *Class loading* - Spring Boot loads classes from JAR
	3. *JIT compilation* - compiler starts interpreting bytecode and compiles hot paths to native machine code for performance 
	4. *Spring context boots*: 
		1. component scan 
		2. auto-configuration
		3. embedded Tomcat start 
		4. `DispatcherServlet` registration
	5. *App is live*

| Aspect              | Local (IntelliJ Run)                                                                                | Production Server                                                       |
| ------------------- | --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **How it starts**   | IntelliJ calls `mvn spring-boot:run` or runs `main()` directly via its own classpath, no JAR needed | `java -jar myapp.jar` on the server, requires the built fat JAR         |
| **Build required?** | No — IntelliJ compiles incrementally and runs from `target/classes`                                 | Yes — `mvn clean package` or `./gradlew bootJar` first                  |
| **JVM instance**    | Your local JDK's JVM, dev-tuned                                                                     | Server JVM, tuned for production (heap size, GC, thread pools)          |
| **Spring Profile**  | Usually `default` or `dev` (H2, verbose logging, DevTools)                                          | `prod` profile via `--spring.profiles.active=prod`                      |
| **DevTools**        | Active — auto-restarts on class change                                                              | Excluded from production builds                                         |
| **Config source**   | `application.properties` / `application-dev.properties`                                             | External config file, env variables, or secrets manager                 |
| **Tomcat**          | Embedded, single-thread friendly, debug port open                                                   | Embedded or external, thread pool tuned, behind a reverse proxy (Nginx) |