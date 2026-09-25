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

## Docker

`Dockerfile` copies a pre-built jar (`mvn clean package` first, then `docker build`) —
simpler than the old monorepo version, since there's no reactor to build from a root
context anymore. See the `infra` repo for the docker-compose setup that runs the whole
cluster.

## Follow-up (not done yet)

- Push a built image to a registry (e.g. GHCR) from CI, instead of building it fresh
  locally every time.
