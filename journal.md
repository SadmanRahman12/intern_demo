# Daily Journal - Spring Boot & PostgreSQL Integration

## What I Worked On Today
- Built and configured a Spring Boot 3 web application using Java 17 and Maven.
- Created the `/hello` REST endpoint returning `"Hello, World!"`.
- Built the `User` entity (`id`, `name`, `email`) mapped to PostgreSQL table `users`.
- Created `UserRepository` extending `JpaRepository<User, Long>` for seamless database access.
- Configured PostgreSQL connection in `application.properties` pointing to local database `intern_demo`.
- Created `UserController` supporting full RESTful CRUD operations (`GET`, `POST`, `PUT`, `DELETE`).
- Developed a modern responsive web dashboard using Thymeleaf templates, CSS glassmorphism, and live API playground.

## Under the Hood: Spring Boot Architecture & Request Flow
```
HTTP Request (e.g. GET /api/users)
       │
       ▼
[Embedded Tomcat Web Server (Port 8080)]
       │
       ▼
[DispatcherServlet (Front Controller)]
       │
       ▼
[UserController (@RestController)] ──> Handles route mapping & request payload
       │
       ▼
[UserRepository (Spring Data JPA Proxy)] ──> Translates Java methods to SQL
       │
       ▼
[Hibernate ORM Engine] ──> Manages SQL syntax & JDBC connection pool (HikariCP)
       │
       ▼
[PostgreSQL Database (intern_demo)] ──> Executes queries on 'users' table
```

## Key Annotations Explained
- `@SpringBootApplication`: Entrypoint annotation combining `@Configuration`, `@EnableAutoConfiguration` (autoconfigures Tomcat, JPA, Jackson based on classpath), and `@ComponentScan`.
- `@RestController`: Specialization of `@Controller` that includes `@ResponseBody`. Methods return domain objects serialized directly as HTTP response bodies (JSON/String) instead of view template names.
- `@Entity` & `@Table(name = "users")`: Defines a JPA persistent domain entity. `@Table(name = "users")` explicitly names the DB table to avoid SQL reserved keyword collisions (`user`).
- `@Id` & `@GeneratedValue(strategy = GenerationType.IDENTITY)`: Marks the primary key field and specifies database column auto-increment generation.
- `@Repository` / `JpaRepository`: Interface extending `JpaRepository` triggers Spring Data JPA auto-proxy creation for CRUD queries without writing boilerplate SQL.
- Constructor Injection: Spring recommended pattern over field `@Autowired` for component dependency management.

## Challenges Faced & Problem Solving
1. **PostgreSQL Reserved Keyword Collision**:
   - *Problem*: Initial queries against table name `user` produced SQL syntax errors in PostgreSQL (`Syntax error near "user"`).
   - *Solution*: Annotated `@Entity` with `@Table(name = "users")` to isolate table names from reserved keywords.
2. **Environment Pathing**:
   - *Problem*: `mvn` command was not registered in system PATH directly.
   - *Solution*: Utilized local Maven binaries at `~/.m2/wrapper/dists/` and explicitly configured `JAVA_HOME` in execution scripts.

## What I Would Do Differently Next Time
- Use Spring Initializr CLI directly for rapid setup.
- Define environment variables for database credentials (`SPRING_DATASOURCE_USERNAME`, `SPRING_DATASOURCE_PASSWORD`) for security best practices.

## Important Links & Resources
- [Java Guides - Spring Boot PostgreSQL JPA Hibernate Tutorial](https://www.javaguides.net/2019/01/springboot-postgresql-jpa-hibernate-crud-restful-api-tutorial.html)
- [Bezkoder - Spring Boot Thymeleaf Example](https://www.bezkoder.com/spring-boot-thymeleaf-example/)
- [Spring Boot Official Documentation](https://spring.io/projects/spring-boot)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
