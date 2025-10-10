# `lockss-parent-pom` Release Notes

## 1.18.0

*   **Features**

    *   Switched from `nexus-staging-maven-plugin` to `central-publishing-maven-plugin`.

*   **Dependencies**

    *   Apache Commons BeanUtils 1.11.0
    *   Apache Commons CLI 1.9.0
    *   Apache Commons Codec 1.18.0
    *   Apache Commons Collections 4.5.0 (Collections4)
    *   Apache Commons Compress 1.27.1
    *   Apache Commons CSV 1.14.0
    *   Apache Commons DBCP2 2.13.0
    *   Apache Commons IO 2.19.0
    *   Apache Commons JXPath 1.4.0
    *   Apache Commons Lang 3.17.0 (Lang3)
    *   Apache Commons Text 1.13.1
    *   Apache Commons Validator 1.9.0
    *   Apache Maven Archetype Plugin 3.3.0
    *   Apache Maven Clean Plugin 3.4.0
    *   Apache Maven Compiler Plugin 3.13.0
    *   Apache Maven Enforcer Plugin 3.5.0
    *   Apache Maven Javadoc Plugin 3.10.1
    *   Apache Maven Install Plugin 3.1.3
    *   Apache Maven Source Plugin 3.3.1
    *   Apache Maven Surefire Plugin 3.4.0
    *   Apache Log4J 2.24.1
    *   Bouncy Castle 1.80
    *   ICU4J 76.1
    *   Jayway JsonPath 2.9.0
    *   JONIX 2025-04
    *   Jsoup 1.20.1
    *   JUnit 5.10.2 (JUnit Platform 1.10.2)
    *   MARC4J 2.9.6
    *   PostgreSQL JDBC Driver 42.7.7
    *   SLF4J 1.7.36
    *   SpotBugs 4.9.3 (SpotBugs Maven Plugin 4.9.3.0)
    *   Other dependency updates (not listed here)

## 1.12.1

### Security

*   Same as 1.12.0 with Jackson-Databind version set to 2.9.10.8, for dependent projects that wish to re-release out of an abundance of caution (CVE-2021-20190).

## 1.12.0

### Features

*   ...

### Fixes

*   ...

## 1.11.0

### Features

*   The Javadoc header is parameterized by `build.java.jarJavadoc.header` (alias: `javadocHeader`).
*   The `jprofiler.agentpath` property can be set to run unit tests with JProfiler.
*   The `useReleaseVersions` profile uses the latest non-snapshot versions of all LOCKSS-related dependencies.
*   Dependent version upgrades:
    *   Hadoop 3.2.0
    *   SolrJ 7.2.1
*   New dependent versions:
    *   Jayway JsonPath 2.4.0

### Fixes

*   The Spring über-JAR now uses the `ZIP` layout.
