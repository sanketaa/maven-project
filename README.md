# Java Maven Multi-Module Project

A small Java web application used to practice Maven project structure, automated testing, build reporting, and Jenkins-oriented CI/CD workflows.

## Background

This repository was created while following James Lee's Jenkins course. It is retained as a hands-on learning project rather than presented as an original production application. The code demonstrates how a Java application can be divided into independently packaged Maven modules and built from one parent configuration.

The project is intentionally simple so the build lifecycle is easy to follow: Java logic is compiled into a JAR, a JSP web module is packaged as a WAR, and unit tests and code-quality reports can run as part of the Maven workflow.

## What the Project Demonstrates

- Parent-and-child Maven POM configuration
- Multi-module dependency and lifecycle management
- Java compilation and JAR packaging
- JSP web application and WAR packaging
- Unit testing with JUnit and Hamcrest
- Test isolation support with Mockito
- Maven site and code-quality reporting
- A build layout suitable for Jenkins pipeline practice

## Architecture

The parent project coordinates two modules:

```text
maven-project
├── server   Java business logic packaged as a JAR
└── webapp   JSP web application packaged as a WAR
```

### Server module

The `server` module contains a small `Greeter` class and unit tests. The tests confirm that the generated greeting contains the supplied name and includes additional greeting text.

### Web application module

The `webapp` module contains a JSP entry page and a Java EE deployment descriptor. Maven packages this module as `webapp.war`.

## Technologies

- Java
- Apache Maven
- JSP and Java Servlet API
- JUnit
- Hamcrest
- Mockito
- Jetty Maven Plugin
- Maven Surefire
- Maven Site
- Checkstyle, PMD, JXR, Javadoc, and FindBugs reporting
- Jenkins-oriented build workflow

## Repository Structure

```text
.
├── pom.xml
├── server
│   ├── pom.xml
│   └── src
│       ├── main/java/com/example/Greeter.java
│       └── test/java/com/example/TestGreeter.java
└── webapp
    ├── pom.xml
    └── src/main/webapp
        ├── index.jsp
        └── WEB-INF/web.xml
```

## Build and Test

### Prerequisites

The project uses an older Java/Maven stack for historical course compatibility:

- JDK compatible with Java 6 source and target settings
- Maven 3.0.3 or later

Modern JDK versions may reject the Java 6 compiler target. If that happens, use a compatible legacy JDK or update the compiler configuration before building.

### Build all modules

```bash
mvn clean package
```

This compiles the Java module, runs its tests, creates `server.jar`, and packages the web module as `webapp.war`.

### Run the tests

```bash
mvn test
```

### Generate the Maven project site

```bash
mvn site
```

The parent POM configures reports for test results, source cross-references, Javadoc, style checks, and static analysis.

### Run the web module with Jetty

```bash
mvn -pl webapp jetty:run
```

The exact command may require an older Maven/JDK combination because the repository pins historical plugin versions.

## CI/CD Learning Value

This repository is useful for demonstrating the basic inputs to a Jenkins Java build:

1. Check out source code from Git.
2. Invoke the Maven lifecycle.
3. Run automated tests.
4. Collect test and quality reports.
5. Archive the JAR and WAR build artifacts.

It shows familiarity with repeatable builds, modular project organization, automated validation, and deployable artifact generation.

## Current Limitations

- The application is a minimal course exercise, not a production service.
- It uses Java 6-era dependencies and Maven plugins.
- The JSP page is static and the web module does not call the server module.
- No Jenkinsfile is included in this repository.
- There is no deployment automation, authentication, database, or API.

## Possible Modernization

- Upgrade the compiler target to a supported Java LTS version.
- Replace legacy Java EE dependencies with Jakarta EE or Spring Boot.
- Add a Jenkinsfile or GitHub Actions workflow.
- Add integration tests between the web and server modules.
- Containerize the WAR deployment.
- Update or replace retired reporting plugins such as FindBugs.

## Attribution

The starting source code is associated with James Lee's Jenkins course. This repository documents the concepts practiced with that course material and does not claim the course example as wholly original work.
