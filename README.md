# Spring Boot Demo

This project includes:
- A simple Hello World REST endpoint at /hello
- A JPA User entity with a repository
- PostgreSQL configuration for local development

## Run locally

1. Start PostgreSQL and create a database named `intern_demo`.
2. Update credentials in `src/main/resources/application.properties` if needed.
3. Run:

```bash
mvn spring-boot:run
```

Then open http://localhost:8080/hello
