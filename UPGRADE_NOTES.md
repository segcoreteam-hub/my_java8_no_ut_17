# Java Version Upgrade Notes

## Target runtime
- Upgraded from Java 8 to **Java 25** (current LTS).
- `pom.xml` sets `maven.compiler.source/target/release = 25`.
- **Builds require JDK 25.** Set `JAVA_HOME` to a JDK 25 installation (e.g.
  `/usr/lib/jvm/java-25-amazon-corretto.x86_64`) in local environments and CI.
  Building with JDK 17 fails with `error: release version 25 not supported`.

## Build plugin version
- `maven-compiler-plugin` is pinned to `3.13.0`, the minimum version able to emit
  Java 25 bytecode. The default plugin version shipped with Apache Maven 3.8.4
  cannot. Verified: `mvn clean package` with Maven 3.8.4 + JDK 25 -> BUILD SUCCESS.

## Dependency updates
- The project declares **no third-party dependencies** (no `<dependencies>` section),
  so no library upgrades (Jackson, Spring Boot, Jakarta EE, Lombok, JDBC drivers, etc.)
  were applicable and none were skipped.
- No `javax.*` imports exist in the sources, so no Jakarta EE namespace migration was needed.
- The project contains no test sources, so no test migration was required.
