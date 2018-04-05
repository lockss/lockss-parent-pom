# Introduction

This Maven project defines a POM file that can be used as the parent POM of
LOCKSS-related projects. **Maven**: `org.lockss:lockss-parent-pom`.

Features that can be turned on include:

*   Generation of a Javadoc JAR.
*   Generation of a sources JAR.
*   GPG signing of build artifacts.
*   Deployment of build artifacts to Sonatype OSSRH.
*   Generation of a Docker image.

# Quick Start

Set your POM's `<parent>` to this POM file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.lockss</groupId>
    <artifactId>lockss-parent-pom</artifactId>
    <version>1.5.0</version>
  </parent>
  
  <groupId>mygroup</groupId>
  <artifactId>myproject</artifactId>
  <version>1.0.0-SNAPSHOT</version>
  <packaging>jar</packaging>

  <name>myproject</name>
  <description>My Project</description>

  <!-- Must be in every lockss-parent-pom/lockss-spring-parent-pom descendant -->
  <scm>
    <connection>${scmConnection}</connection>
    <developerConnection>${scmDeveloperConnection}</developerConnection>
    <url>${scmUrl}</url>
  </scm>
  
</project>  
```

# Customizing the Build

## Javadoc JAR

The Javadoc JAR is not built unless the `lockss-release` profile is active or
`skipJavadoc` is set to `false`.

## Sources JAR

The sources JAR is not built unless the `lockss-release` profile is active or
`skipSources` is set to `false`.

## GPG Signatures

The build artifacts are not GPG signed unless the `lockss-release` profile is
active or `skipGpg` is set to `false`.

## Deployment to OSSRH

The build artifacts are not deployed to OSSRH unless the `lockss-release`
profile is active.

## Docker Image

*Under construction*

# Bundles

This POM file defines properties that make it easy to switch between versions
of other LOCKSS dependency bundles:

*   `lockss.core.version`
*   `lockss.spring-boot.version`
*   `lockss.junit4.version`
*   `lockss.junit5.version`

The bundles below are not part of this POM but are described here for
convenience.

## `lockss-core` Bundle

To bring in the `lockss-core` bundle, add this dependency to your POM:

```xml
    <dependency>
      <groupId>org.lockss</groupId>
      <artifactId>lockss-core-bundle</artifactId>
      <version>${lockss.core.version}</version>
      <type>pom</type>
    </dependency>
```

## `lockss-core` Bundle

To bring in the `lockss-core` bundle, add this dependency to your POM:

```xml
    <dependency>
      <groupId>org.lockss</groupId>
      <artifactId>lockss-core-bundle</artifactId>
      <version>${lockss.core.version}</version>
      <type>pom</type>
    </dependency>
```

## Spring Boot Bundle

To bring in the Spring Boot bundle, add this dependency to your POM:

*Under construction*

## JUnit 4 Bundle

To bring in the JUnit 4 bundle, add this dependency to your POM:

```xml
    <dependency>
      <groupId>org.lockss</groupId>
      <artifactId>lockss-junit4-bundle</artifactId>
      <version>${lockss.junit4.version}</version>
      <type>pom</type>
    </dependency>
```

## JUnit 5 Bundle

To bring in the JUnit 5 bundle, add this dependency to your POM:

```xml
    <dependency>
      <groupId>org.lockss</groupId>
      <artifactId>lockss-junit5-bundle</artifactId>
      <version>${lockss.junit5.version}</version>
      <type>pom</type>
    </dependency>
```

