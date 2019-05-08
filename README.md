# lockss-parent-pom

`lockss-parent-pom` is a Maven POM file used to define and drive the build
infrastructure common to LOCKSS projects.

*This Git repository uses a Git Flow layout, where the `master` branch contains
stable releases and main development is carried out in the `develop` branch.*

## Build Overview

### Info Build

The info build gathers and outputs information about the build environment.

*   Driving property: `build.info.skip`
*   Alias: `skipInfo`
*   Default: `false` (info build is on by default)

### Java Build

The Java build compiles, tests and packages a Java project, with optional build
sub-parts.

*   Driving property: `build.java.skip`
*   Alias: `skipJava`
*   Default: `true` (Java build is on by default)

#### ANTLR Portion

The Java build has an optional ANTLR portion, which generates parsers from ANTLR
grammars in the `src/main/resources` tree.

*   Driving property: `build.java.antlr.skip`
*   Alias: `skipAntlr`
*   Default: `false` (ANTLR portion is off by default)

#### Database Portion

The Java build has an optional database portion, which can process the
versioning of a database schema with Flyway migrations in
`src/main/resources/db`, and generate database object code with JOOQ in the
`src/generated/java` tree.

*   Driving property: `build.java.db.skip`
*   Alias: `skipDb`
*   Default: `false` (database portion is off by default)

#### Spring Portion

The Java build has an optional Spring portion which can generate a Spring
application with Swagger Codegen from a Swagger 2 or OpenAPI 3 specification in
`src/main/resources/swagger/swagger.yaml` into the `src/generated/java` tree,
and generate a JAR with dependencies ("fat JAR" or "über JAR") for Spring Boot.

*   Driving property: `build.java.spring.skip`
*   Alias: `skipSpring`
*   Default: `false` (Spring portion is off by default)

### Docker Build

The Docker build packages the Java project as a Docker image, from a
`Dockerfile` specification.

*   Driving property: `build.docker.skip`
*   Alias: `skipDocker`
*   Default: `true` (Docker build is off by default)

## Profile-Based Tasks

Various canned operations, like doing releases or running a tool over the
project, are packaged as profiles.

### Doing a Snapshot Release

To perform a snapshot release:

```
mvn -U -P doSnapshot
```

### Doing a Release

To perform a release:

```
mvn -U -P doRelease
```

### Generating REST API Documentation

To generate an HTML page documenting the REST API described by the Swagger 2 or
OpenAPI 3 specification in `src/main/resources/swagger/swagger.yaml`:

```
mvn -P doRestApiDocs
```

The result is in `target/generated-sources/swagger/index.html`.

## Inheriting from `lockss-parent-pom`

A project inheriting from `lockss-parent-pom` but not under the auspices of the
LOCKSS Program should override the following sections:

*   `<url>`
*   `<inceptionYear>`
*   `<organization>`
*   `<licenses>`
*   `<developers>`
*   `<contributors>`

All descendant projects must include the `<scm>` section:

```
  <!-- Must be in every lockss-parent-pom descendant -->
  <scm>
    <connection>${scmConnection}</connection>
    <developerConnection>${scmDeveloperConnection}</developerConnection>
    <url>${scmUrl}</url>
  </scm>
```

The default assumption is a project hosted on GitHub, under the organization
name `lockss`, with a project name matching the Maven project artifact ID, with
`scmConnection`, `scmDeveloperConnection` and `scmUrl` assembled from
`gitSshUsername`, `gitHost`, `gitGroupId`, `gitProjectId` and
`gitParentProjectId` (see details in the file).

### Enabling the ANTLR Portion

To enable the ANTLR portion, set:

```
    <build.java.antlr.skip>false</build.java.antlr.skip>
```

### Enabling the Spring Portion

To enable the Spring portion, set:

```
    <build.java.spring.skip>false</build.java.spring.skip>
```

and supply a package name and main class name, e.g.:

```
    <build.java.package>com.exmaple.app</build.java.package>
    <build.java.mainClass>${build.java.package}.MyApplication</build.java.mainClass>
```

### Enabling the Docker Build

To enable the Docker build, set:

```
    <build.docker.skip>false</build.docker.skip>
```

and optionally supply a service port if your application is listening on one,
e.g.:

```
    <build.docker.dockerBuild.servicePort>12345</build.docker.dockerBuild.servicePort>
```

## Pre-Defined Properties

Various directories and file paths are parameterized as `dir.*` and `file.*`
respectively.

Many version numbers are parameterized as `version.group.*` (multi-JAR projects
with grouped versioning: JUnit, Spring, Jackson, etc.), `version.plugin.*`
(Maven plugins), `version.lockss.*` (LOCKSS components), and
`version.dependency.*` (typical dependencies: Apache
Commons, etc.).

See the `<properties>` section for details.

## Style Guide

The ordering of most elements in a POM file has no effect. For consistency, the
preferred ordering for LOCKSS projects is that of the Maven model
documentation page (http://maven.apache.org/ref/3.6.0/maven-model/maven.html).

## Links

*   [LOCKSS Program on GitHub](https://github.com/lockss)
*   [LOCKSS Documentation Portal on GitHub Pages](https://lockss.github.io/)
*   [LOCKSS Program website](https://www.lockss.org/)
