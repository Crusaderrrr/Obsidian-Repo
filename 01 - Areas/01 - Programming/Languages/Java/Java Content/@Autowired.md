---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
  - spring
note type: Informational Note
---
##  `@Autowired`

- Used for dependency injection
- Spring itself injects all the dependencies to a Bean.
- Its functionality depends on where is pasted (class, constructor, setter)

**Steps**:
1. Scan all `@Component` beans and create them.
2. Scan all created beans and check if if any fits to the `@Autowired`
3. If found -> inject
4. If not found -> error 
5. If many found -> **ambiguity**

*Example* (both dependencies will be injected):
```java
@Component
public class MusicPlayer {
  private ClassicalMusic classicalMusic;
  private RockMusic rockMusic;

  @Autowired
  public MusicPlayer(ClassicalMusic classicalMusic, RockMusic rockMusic) {
    this.classicalMusic = classicalMusic;
    this.rockMusic = rockMusic;
  }

  public void playMusic() {
    System.out.println(classicalMusic.getSong());
    System.out.println(rockMusic.getSong());
  }
}
```
