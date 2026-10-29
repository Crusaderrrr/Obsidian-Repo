**In general we should upgrade by 1 major version at a time.**

The process:
1. *Find out where you actually are*
```bash
mvn dependency:tree -Dincludes=com.example:the-lib # lists all deps
# Gradle:
./gradlew dependencyInsight --dependency the-lib # concrete dependency check
```

2. *Read the release notes and migration guides for every major in between*
	For many things exist docs that explain how to properly upgrade from version X to version Y

3. *Clear deprecations first*
	Move to last minor version of the current major and fix all the deprecation warnings

4. *Bump one major and get it green*
	- **OpenRewrite** (Java tool) has some features that help on migrations, for example rename javax -> jakarta

5. *Don’t trust “it compiles.”*
	There’s a gap between _source_ compatibility and _binary_ compatibility. Your code may compile fine against v5. But if another jar on your classpath was compiled against v2, it can fail at runtime with `NoSuchMethodError` or `NoClassDefFoundError`


### Interesting 
We can actually check if a method exists in the jar of a new version we are aiming by:
`javap -public -cp the-lib.jar com.example.Client` 