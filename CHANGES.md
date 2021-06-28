# `lockss-parent-pom` Release Notes

## Changes Since 1.12.0

*   ...

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
