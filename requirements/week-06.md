# Week 06: Low-Level Requirements (User Management Service - Part 2: JWT & Auth)

## 1. JWT (JSON Web Token) Implementation
- [ ] Research: What is JWT? Structure (Header, Payload, Signature). How it's used for stateless authentication.
- [ ] Add JWT library dependency (e.g., `io.jsonwebtoken:jjwt-api`, `jjwt-impl`, `jjwt-jackson`).
- [ ] Create a `JwtUtil` or `JwtTokenProvider` class:
    - [ ] Method to generate a JWT token from user details (e.g., username, roles).
        - Define a secret key (store securely, e.g., in application properties).
        - Set expiration time.
    - [ ] Method to validate a JWT token.
        - Check signature, expiration.
    - [ ] Method to extract username (subject) from a token.
    - [ ] Method to extract claims (e.g., roles) from a token.
- [ ] Store the JWT secret key securely in `application.properties` (e.g., `app.jwt.secret`). Avoid hardcoding in Java classes.
- [ ] Define JWT expiration time in `application.properties` (e.g., `app.jwt.expiration-ms`).

## 2. Login Endpoint and Token Generation
- [ ] Create a DTO for login request (e.g., `LoginRequest` with `username` and `password`).
- [ ] Implement a login endpoint (e.g., **POST** `/api/auth/login` or `/api/users/login`):
    - Takes `LoginRequest` as `@RequestBody`.
    - Authenticate the user using Spring Security's `AuthenticationManager`.
        - Inject `AuthenticationManager` into your controller/service.
        - Create `UsernamePasswordAuthenticationToken` and pass to `authenticationManager.authenticate()`.
    - If authentication is successful, generate a JWT token using your `JwtUtil`.
    - Return the JWT token in the response (e.g., in a `LoginResponse` DTO).
- [ ] If authentication fails, Spring Security will typically handle returning a 401 Unauthorized, but ensure this behavior.

## 3. JWT Authentication Filter
- [ ] Create a custom JWT authentication filter (e.g., `JwtAuthenticationFilter extends OncePerRequestFilter`).
    - This filter will run for every request.
    - In `doFilterInternal`:
        - Extract the JWT token from the `Authorization` header (Bearer token).
        - If token exists and is valid (use `JwtUtil`):
            - Extract username and roles from the token.
            - Create an `UsernamePasswordAuthenticationToken` with user details (username, null for credentials, authorities/roles).
            - Set this token in `SecurityContextHolder.getContext().setAuthentication(authentication)`.
- [ ] Configure Spring Security to use this filter:
    - Add the `JwtAuthenticationFilter` before a standard Spring Security filter (e.g., `UsernamePasswordAuthenticationFilter`) in your `SecurityConfig`.
    - Ensure your security configuration is stateless (`http.sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))`).
- [ ] Update `SecurityConfig` to permit access to login/registration endpoints (`/api/auth/**`) without authentication, and secure other endpoints.

## 4. Securing Endpoints & Role-Based Authorization
- [ ] Create a test endpoint (e.g., **GET** `/api/users/me`) that returns the details of the currently authenticated user.
    - Inject `Authentication` principal or use `SecurityContextHolder` to get user details.
    - This endpoint should be accessible only to authenticated users.
- [ ] Implement basic role-based access control (RBAC):
    - Ensure users have roles assigned during registration (e.g., "ROLE_USER" by default).
    - Create an admin-only endpoint (e.g., **GET** `/api/admin/users` to list all users - implement pagination later).
    - Secure this endpoint using `@PreAuthorize("hasRole('ADMIN')")` or `http.authorizeHttpRequests(auth -> auth.requestMatchers("/api/admin/**").hasRole("ADMIN"))`.
- [ ] Test:
    - Accessing protected endpoints without a token (expect 401/403).
    - Accessing protected endpoints with a valid token.
    - Accessing admin endpoints as a regular user (expect 403).
    - Accessing admin endpoints as an admin user (requires a way to create an admin user, e.g., via data loader or a special registration).

## 5. Token Handling Considerations
- [ ] Discuss (no implementation needed this week, but be aware):
    - Token storage on the client-side (localStorage, sessionStorage, cookies). Pros and cons.
    - Token refresh mechanisms.
    - Token revocation/blacklisting (though this makes it less stateless).
- [ ] Update `User` entity to properly store roles if using a `Role` entity and `@ManyToMany` (this might be a carry-over from Week 5 if not fully implemented).

## 6. Unit and Integration Tests
- [ ] Write unit tests for `JwtUtil` (token generation, validation, claim extraction - may need a library like Mockito for date/time).
- [ ] Write integration tests for the login endpoint.
- [ ] Write integration tests for accessing protected endpoints with and without JWT tokens.
    - Use `@SpringBootTest` and `TestRestTemplate` or `MockMvc`.
    - Use `@WithMockUser` or manually set Authorization header for testing secured endpoints.

## Code Refinement
- [ ] Review all new code for clarity, security considerations, and best practices.
- [ ] Add Javadoc and logging.
- [ ] Commit changes frequently.
