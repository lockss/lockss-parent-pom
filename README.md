# lockss-parent-pom

`lockss-parent-pom` is a Maven POM file used to define and drive the build
infrastructure common to LOCKSS projects.

It can be used to make Java builds, with conditional build activities for
LOCKSS Spring Boot services and Docker images, and optional build activities to
deploy to Maven Central and Docker Hub, generate REST API documentation, and
more.

This Git repository uses a Git Flow layout, where the `master` branch contains
stable releases and main development is carried out in the `develop` branch.

## Build Overview

### Default Build

By default, the build is a Java build, producing:

*   A main JAR.
    *   Classifier: none.
    *   Symbolic link: `target/current.jar`.
*   A sources JAR.
    *   Classifier `sources`.
    *   Plugin: `maven-source-plugin`.
    *   Suppress by setting `skipSources` to `true`.
*   A Javadoc JAR.
    *   Classifier `javadoc`.
    *   Plugin: `maven-javadoc-plugin`.
    *   Suppress by setting `skipJavadoc` to `true`.

### Test JAR

If you set `skipTestJar` to `false`, the build also produces:

*   A test JAR.
    *   Classifier: `tests`.
    *   Symbolic link: `target/current-tests.jar`.

### Spring Boot Build

If you set `skipSpringBootRepackage` to `false`, the project is assumed to be
a LOCKSS Spring Boot service, and the build also produces:

*   A JAR with dependencies.
    *   Classifier: `with-deps`.
    *   Plugin: `spring-boot-maven-plugin`.
    *   Symbolic link: `target/current-with-deps.jar`.

Note that `skipSpringBootRepackage` may be renamed in a future version.

### Docker Build

If you set `skipDocker` to `false`, the project is assumed to have a
`Dockerfile`, and the build also produces:

*   A Docker image.
    *   Docker must be running. This is checked in the `validate` phase by a
        plugin execution named `check-docker`.
    *   This type of Docker build requires two build arguments.
        *   Set `dockerServicePort` to the REST service port.

### GPG Signing

If `skipGpg` is set to `false`, the project's artifacts are also signed with
GnuPG.

### Release Profile

The `lockss-release` profile 

## Inheriting from `lockss-parent-pom`

A project inheriting from `lockss-parent-pom` will typically look like this:

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.lockss</groupId>
    <artifactId>lockss-parent-pom</artifactId>
    <version>...</version>
  </parent>

  <groupId>...</groupId>
  <artifactId>...</artifactId>
  <version>...</version>
  <packaging>jar</packaging>

  <!-- Must be in every lockss-parent-pom descendant -->
  <scm>
    <connection>${scmConnection}</connection>
    <developerConnection>${scmDeveloperConnection}</developerConnection>
    <url>${scmUrl}</url>
  </scm>

  <properties>
    <!-- ... properties ... -->
  </properties>

  <dependencies>
    <!-- ... dependencies ... -->
  </dependencies>

  <build>
    <!-- ... build ... -->
  </build>

</project>
```

### `<scm>` Section

All descendant projects must have a copy of the `<scm>` section:

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
`gitSshUsername`, `gitHost`, `gitGroupId` and `gitProjectId` like so:

```
    <gitSshUsername>git</gitSshUsername>
    <gitHost>github.com</gitHost>
    <gitGroupId>lockss</gitGroupId>
    <gitProjectId>${project.artifactId}</gitProjectId>
    <scmConnection>scm:git:git://${gitHost}/${gitGroupId}/${gitProjectId}.git</scmConnection>
    <scmDeveloperConnection>scm:git:${gitSshUsername}@${gitHost}:${gitGroupId}/${gitProjectId}.git</scmDeveloperConnection>
    <scmUrl>https://${gitHost}/${gitGroupId}/${gitProjectId}</scmUrl>
```

Projects whose Maven project artifact ID does not match the Git project name
need to set `gitProjectId`, as well as `gitGroupId` if under a different GitHub
user name or organization name.

### `<licenses>` Section

By default, descendant projects inherit a `<licenses>` section containing the
LOCKSS Program's preferred software license (3-Clause BSD License):

```
  <licenses>
    <license>
      <name>3-Clause BSD License</name>
      <url>https://opensource.org/licenses/BSD-3-Clause</url>
    </license>
  </licenses>
```

If your descendant project uses other licensing, you will need to define your
own `<licenses>` section.

### Organizational Boilerplate

By default, descendant projects inherit the LOCKSS Program's organizational
boilerplate (project URL, project inception year, organization name and URL,
list of developers and contributors):

```
  <url>https://www.lockss.org/</url>
  <inceptionYear>2000</inceptionYear>
  
  <organization>
    <name>LOCKSS Program</name>
    <url>https://www.lockss.org/</url>
  </organization>
  
  <developers>
    <!-- ... list of LOCKSS Program developers ... -->
  </developers>

  <contributors>
    <!-- ... list of LOCKSS Program contributors ... -->
  </contributors>
```

If your descendant project does not fall under the LOCKSS Program, you will need
to define your own organizational boilerplate accordingly.

## Style Guide

The ordering of most elements in a POM file has no effect. For consistency, the
preferred ordering for LOCKSS projects is that of the Maven model
documentation page (http://maven.apache.org/ref/3.6.0/maven-model/maven.html).

## Links

*   [LOCKSS Program on GitHub](https://github.com/lockss)
*   [LOCKSS Documentation Portal on GitHub Pages](https://lockss.github.io/)
*   [LOCKSS Program website](https://www.lockss.org/)
