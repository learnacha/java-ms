# Week 04: Low-Level Requirements

## 1. Docker Compose for Multi-Container Applications
- [ ] Research: What is Docker Compose? How does it simplify multi-container setups?
- [ ] Install Docker Compose (usually included with Docker Desktop).
- [ ] Create a `docker-compose.yml` file for the MarketPlace Pro project.
    - [ ] Define a service for your Spring Boot application (e.g., `marketplace-pro-app`).
        - Use the Docker image built in Week 3.
        - Configure port mapping.
        - Set up environment variables if needed (e.g., Spring profiles).
    - [ ] Define a service for a PostgreSQL database (e.g., `postgres-db`).
        - Use an official PostgreSQL image (e.g., `postgres:latest`).
        - Configure environment variables for database name, user, and password.
        - Set up a volume to persist PostgreSQL data.
    - [ ] Configure the application service to depend on the database service.
- [ ] Update `application-prod.properties` (or a new `application-docker.properties`) in your Spring Boot app to connect to the PostgreSQL container.
    - Ensure JDBC driver for PostgreSQL is in `pom.xml`/`build.gradle`.
- [ ] Run `docker-compose up`.
- [ ] Test if the application connects to the PostgreSQL database and performs CRUD operations.
- [ ] Learn Docker Compose commands: `docker-compose down`, `docker-compose logs`, `docker-compose ps`.

## 2. Migrating to PostgreSQL (from H2)
- [ ] If not already done for Docker Compose setup, ensure PostgreSQL JDBC driver is in your project.
- [ ] Update `Product` entity and JPA configurations if necessary for PostgreSQL compatibility (though usually minimal changes are needed from H2).
- [ ] Change Spring Boot datasource configuration in `application.properties` (or a profile like `application-dev.properties`) to point to a local PostgreSQL instance (can be one running via Docker Compose or installed separately).
    - Configure URL, username, password.
- [ ] Test all CRUD operations for the `Product` service against PostgreSQL.
- [ ] Verify data persistence in PostgreSQL using a DB tool (e.g., pgAdmin, DBeaver, IntelliJ Database tools).

## 3. Advanced Error Handling & Validation
- [ ] Implement global error handling using `@ControllerAdvice` and `@ExceptionHandler`.
    - Create custom exception classes (e.g., `ResourceNotFoundException`).
    - Handle common exceptions like `MethodArgumentNotValidException` for validation failures.
- [ ] Add validation to your `Product` entity's fields using Jakarta Bean Validation annotations (e.g., `@NotBlank`, `@Min`, `@Max`, `@Size`).
    - Ensure `@Valid` is used in controller methods receiving these objects.
- [ ] Test error handling and validation (e.g., sending invalid data, requesting non-existent resources).

## 4. Introduction to CI/CD with GitHub Actions
- [ ] Research: Basic concepts of CI/CD (Continuous Integration/Continuous Delivery or Deployment).
- [ ] Create a simple GitHub Actions workflow file (e.g., `.github/workflows/build-test.yml`).
    - [ ] Define triggers (e.g., on push to `main` or `develop` branch, on pull requests).
    - [ ] Set up a job that runs on an Ubuntu runner.
    - [ ] Steps:
        - Checkout code (`actions/checkout@v3`).
        - Set up JDK (`actions/setup-java@v3`).
        - Build the application (e.g., `mvn clean install` or `gradle build`).
        - Run tests (tests should execute as part of the build).
- [ ] Commit the workflow file and push to GitHub to trigger the action.
- [ ] Observe the workflow execution in the "Actions" tab on GitHub.
- [ ] (Optional) Add a step to build the Docker image (without pushing to a registry yet).

## 5. Refine and Document Existing Service
- [ ] Review the `Product` service code for any improvements.
- [ ] Add comprehensive Javadoc to all public classes and methods.
- [ ] Ensure logging is sufficient for debugging and monitoring.
- [ ] Update `README.md` for the project:
    - How to build and run the project.
    - How to run with Docker and Docker Compose.
    - Available API endpoints (consider generating API documentation next phase).
- [ ] Ensure all dependencies are up-to-date and address any known vulnerabilities (e.g., using `mvn dependency-updates-report` or `gradle dependencyUpdates`).
