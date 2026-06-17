# CLAUDE.md

## Project purpose
A car repair shop management web application: managers assign car service tasks to mechanics, and the system tracks cars, tasks, statuses, and types. (Final project for Coding Factory 5.)

## Tech stack
- Java 17, Spring Boot 3.3.0 (Maven)
- Spring MVC (REST + Thymeleaf web pages), Spring Data JPA, Spring Security, Spring Validation
- MySQL (mysql-connector-j 8.3.0)
- Lombok
- springdoc-openapi (Swagger UI)
- Frontend: Thymeleaf templates + static CSS; WebJars for Vue 2.6.11 and Axios

## Build / run / test
- Build: `mvn clean package`
- Run: `mvn spring-boot:run` (or run `CarRepairShopApplication`)
- App serves on port `8085`
- Swagger UI: http://localhost:8085/swagger-ui/index.html
- Requires a local MySQL database named `car_service` on `localhost:3306`. Configure credentials in `src/main/resources/application.properties` (currently `username=root`, `password=DB_PASSWORD` placeholder).
- No test sources are present in the repo.

## Key directories
- `src/main/java/com/mixalismavromanolakis/car_service_tasks/`
  - `CarRepairShopApplication.java` — Spring Boot entry point
  - `RestControllers/` — REST API endpoints (Car, Mechanic, Status, Task, Type, MainPage)
  - `WebPageControllers/` — Thymeleaf page controllers (login, register, dashboards, errors)
  - `Repositories/` — Spring Data JPA repositories
  - `DTO/`, `EntityConverter/`, `Mapper/`, `UIConverter/` — data transfer and conversion layers
  - `config/` — `OpenApiConfig` (Swagger configuration)
- `src/main/resources/`
  - `templates/` — Thymeleaf HTML views (+ `fragments/`)
  - `static/css/` — stylesheets
  - `db/migration/` — versioned SQL scripts (V1..V10)
  - `application.properties` — datasource and JPA/server config

## Notable conventions
- Package directories use PascalCase (e.g. `RestControllers`, `Repositories`, `DTO`), which is unusual for Java.
- `spring.jpa.hibernate.ddl-auto=update` is set, so Hibernate manages schema; the `db/migration` SQL scripts exist but Flyway is not declared as a dependency in `pom.xml`.
- DB password in `application.properties` is a placeholder (`DB_PASSWORD`) and must be set before running.
