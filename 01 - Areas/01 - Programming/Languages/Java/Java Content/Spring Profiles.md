---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - java
  - programming
  - spring
note type: Informational Note
---
Spring profiles in Spring framework (especially Spring Boot) are a core feature that allow developers to segregate parts of the application configuration and **beans** so they are activated or **loaded** only in **specific environments**.

*Key points*:
- A **profile represents** a specific set of configuration values, beans, and settings tailored for an environment such as **dev**, **test**, **prod**.
- Developers create profile-specific configuration files like `application-dev.properties`, `application-prod.yml`, etc., which contain settings relevant to that profile.
- Beans can be annotated with `@Profile("dev")` or `@Profile("prod")`, etc., so they are only instantiated when the corresponding profile is active.
- The active profile(s) can be set in the configuration file (`spring.profiles.active=dev`) or overridden at runtime via command-line arguments or programmatically.