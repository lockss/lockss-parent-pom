# Release Notes

## Major Changes Since 1.11.0

*   (highlights go here)

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
