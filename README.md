# discovery-server

Eureka service registry for Project Nexus's microservices. Extracted from the original
monorepo into its own standalone project, per the course's polyrepo requirement (each
microservice its own repo, its own independent Spring Boot project). No dependency on
`common-libs` — this service is self-contained.

## Build & test

```bash
mvn clean package
```

## Run

```bash
java -jar target/discovery-server-0.1.0-SNAPSHOT.jar
```

Serves the Eureka dashboard on port 8761 by default. Every other service
(`api-gateway`, `user-service`, `catalog-service`, ...) registers with this instance via
`eureka.client.serviceUrl.defaultZone` in its own `application.yml` — start this one
first.

## Follow-up (not done yet)

- Set up this repo's own CI/CD pipeline (build, test, Docker image, push to a registry).
- `Dockerfile` in this repo can be simplified since this is no longer a multi-module
  reactor — a plain single-project Docker build context now works.
