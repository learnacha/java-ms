# Week 03: Low-Level Requirements

## 1. Introduction to Docker & Containerization
- [ ] Research: What is Docker? Key concepts (Images, Containers, Dockerfile, Docker Hub).
- [ ] Install Docker Desktop (or Docker Engine on Linux).
- [ ] Verify Docker installation (`docker --version`, `docker run hello-world`).
- [ ] Create a `Dockerfile` for the Spring Boot application (MarketPlace Pro).
    - [ ] Use a suitable base image (e.g., `openjdk:21-jdk-slim`).
    - [ ] Add commands to copy the packaged `.jar` file.
    - [ ] Specify the `ENTRYPOINT` or `CMD` to run the application.
- [ ] Build a Docker image from the `Dockerfile` (`docker build -t marketplace-pro .`).
- [ ] Run the application as a Docker container (`docker run -p 8080:8080 marketplace-pro`).
- [ ] Test the containerized application by accessing its endpoints.
- [ ] Learn basic Docker commands: `docker ps`, `docker images`, `docker stop <container_id>`, `docker rm <container_id>`, `docker rmi <image_id>`.
- [ ] (Optional) Push the Docker image to Docker Hub or another container registry.

## 2. Spring Boot Actuator
- [ ] Research: What is Spring Boot Actuator? What are its benefits?
- [ ] Add `spring-boot-starter-actuator` dependency to the project.
- [ ] Explore default Actuator endpoints (e.g., `/actuator/health`, `/actuator/info`, `/actuator/metrics`).
    - [ ] Understand how to enable and expose more endpoints (e.g., `management.endpoints.web.exposure.include=*`).
- [ ] Customize the `/actuator/info` endpoint to display application information (e.g., build version, custom properties).
- [ ] Secure Actuator endpoints (e.g., by integrating with Spring Security or using different management port). This might be a stretch goal or covered more deeply when Spring Security is introduced.

## 3. Externalized Configuration & Spring Profiles
- [ ] Research: Importance of externalized configuration.
- [ ] Understand Spring Boot's property loading order (e.g., `application.properties`, environment variables, command-line arguments).
- [ ] Create different profile-specific property files (e.g., `application-dev.properties`, `application-prod.properties`).
    - [ ] Example: Use H2 for `dev` and configure for PostgreSQL (without actually setting it up yet) for `prod`.
    - [ ] Example: Different server ports for different profiles.
- [ ] Learn how to activate Spring profiles (e.g., via `spring.profiles.active` property or environment variable).
- [ ] Test running the application with different active profiles and verify configurations are loaded correctly.
- [ ] Use `@Value` and `@ConfigurationProperties` to inject configuration into beans.

## 4. Integration Testing
- [ ] Research: Difference between unit tests and integration tests.
- [ ] Write integration tests for the `ProductRepository` (Spring Data JPA).
    - [ ] Use `@DataJpaTest` annotation.
    - [ ] Test saving, retrieving, updating, and deleting products.
    - [ ] Verify interactions with the H2 database.
- [ ] Write integration tests for the `ProductService` (if a separate service layer exists) or `ProductController` focusing on the full request-response cycle with a real database connection.
    - [ ] Use `@SpringBootTest` with `webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT`.
    - [ ] Use `TestRestTemplate` or `MockMvc` (if focusing on web layer integration without full server startup).
    - [ ] Test CRUD operations from the API endpoint down to the database.
- [ ] Ensure tests clean up after themselves (e.g., using `@DirtiesContext` or manual cleanup if needed).

## 5. Code Refinement and Best Practices
- [ ] Review existing code for clarity, efficiency, and adherence to conventions.
- [ ] Add Javadoc comments to public methods and classes.
- [ ] Ensure proper logging is in place (e.g., using SLF4J with Logback).
- [ ] Commit changes regularly with clear and descriptive messages.
