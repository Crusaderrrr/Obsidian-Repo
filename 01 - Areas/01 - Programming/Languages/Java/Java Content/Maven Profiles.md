---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
**Maven profiles** provide a flexible approach to adapt the build process for different environments (e.g., development, testing, production) or build scenarios (e.g., skipping tests, including extra plugins).

**Key traits**:
- Can be global `settings.xml` or local `pom.xml`
- Can be activated depending on the file presence, OS, JDK version, property setting.
- Used to control the application behavior 