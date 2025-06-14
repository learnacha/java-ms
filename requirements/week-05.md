# Week 05: Low-Level Requirements (User Management Service - Part 1)

## 1. Project Setup for User Management Service
- [ ] Create a new Spring Boot project for the User Management Service (e.g., `user-management-service`).
    - Use Spring Initializr (start.spring.io).
    - Dependencies: Spring Web, Spring Data JPA, PostgreSQL Driver, Lombok (optional), Spring Boot DevTools (optional).
- [ ] Set up the project in your IDE.
- [ ] Configure basic application properties (`application.properties`):
    - Server port (choose a different port than the Product service, e.g., 8081).
    - Application name (`spring.application.name=user-management-service`).
- [ ] Create a main application class (e.g., `UserManagementServiceApplication.java`).
- [ ] Initialize a Git repository for this new service (or manage as a module within a monorepo, though separate repo is simpler for now).
    - Create a `.gitignore` file.

## 2. Database Setup (PostgreSQL)
- [ ] Ensure you have a PostgreSQL instance running (local or Dockerized from Week 4).
- [ ] Create a new database or schema specifically for the User Management service (e.g., `user_management_db`).
- [ ] Configure datasource properties in `application.properties` to connect to this database:
    - `spring.datasource.url` (e.g., `jdbc:postgresql://localhost:5432/user_management_db`)
    - `spring.datasource.username`
    - `spring.datasource.password`
    - `spring.jpa.hibernate.ddl-auto=update` (for development; consider `validate` or Flyway/Liquibase later).
- [ ] Test the database connection by running the Spring Boot application.

## 3. User Entity and Repository
- [ ] Define a `User` entity (e.g., in `com.example.usermanagement.model` package):
    - `id` (Long, auto-generated)
    - `username` (String, unique, not blank)
    - `password` (String, not blank)
    - `email` (String, unique, not blank, valid email format)
    - `firstName` (String)
    - `lastName` (String)
    - `roles` (Set of Strings or a `Role` Entity - for now, a simple `String` like "ROLE_USER", "ROLE_ADMIN" stored perhaps as a comma-separated string or a separate table if using `@ElementCollection` or `@ManyToMany` with `Role` entity later). Start simple.
    - `createdAt`, `updatedAt` (timestamps).
- [ ] Use JPA annotations (`@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`, etc.).
- [ ] Add Jakarta Bean Validation annotations (`@NotBlank`, `@Email`, `@Size`) to fields.
- [ ] Create a `UserRepository` interface extending `JpaRepository<User, Long>` (e.g., in `com.example.usermanagement.repository`).
    - Add custom query methods if needed (e.g., `findByUsername(String username)`, `findByEmail(String email)`).

## 4. Introduction to Spring Security
- [ ] Add `spring-boot-starter-security` dependency to `pom.xml` or `build.gradle`.
- [ ] Create a basic Spring Security configuration class (e.g., `SecurityConfig extends WebSecurityConfigurerAdapter` or using the new component-based approach with `SecurityFilterChain` bean - prefer new approach for Spring Boot 3+).
    - [ ] For now, configure it to protect all endpoints by default (requiring basic auth, which will be replaced by JWT later).
    - [ ] Define a `PasswordEncoder` bean (e.g., `BCryptPasswordEncoder`).
- [ ] Observe that your application now requires basic authentication for all endpoints.

## 5. User Registration API
- [ ] Create a `UserController` or `AuthController` (e.g., in `com.example.usermanagement.controller`).
- [ ] Create a DTO (Data Transfer Object) for user registration (e.g., `UserRegistrationRequest`) with fields like `username`, `password`, `email`, `firstName`, `lastName`.
- [ ] Implement a public registration endpoint (e.g., **POST** `/api/auth/register` or `/api/users/register`):
    - Takes `UserRegistrationRequest` as `@RequestBody`.
    - Validate the request DTO (`@Valid`).
    - Check if username or email already exists using `UserRepository`. Return appropriate error (e.g., 409 Conflict).
    - Encode the password using the `PasswordEncoder`.
    - Create a new `User` entity and save it using `UserRepository`.
    - Return a success response (e.g., 201 Created with user details (excluding password) or a success message).
- [ ] Create a DTO for representing User details in responses (e.g., `UserResponse`) to avoid exposing the password.
- [ ] Test the registration endpoint using Postman or `curl`. Verify user creation in the database.

## 6. Basic Exception Handling for User Service
- [ ] Implement `@ControllerAdvice` for the User Management service.
- [ ] Handle potential exceptions:
    - `DataIntegrityViolationException` (e.g., for duplicate username/email if not caught before saving).
    - Custom exceptions like `UserAlreadyExistsException`.
    - `MethodArgumentNotValidException` for DTO validation.

## Project Structure and Commits
- [ ] Organize code into packages (model, repository, controller, service (optional for now), config, dto).
- [ ] Commit changes frequently with descriptive messages.
