# Week 02: Low-Level Requirements

## 1. Advanced REST API Concepts
- [ ] Research: REST principles (Statelessness, Client-Server, Cacheable, Uniform Interface, Layered System).
- [ ] Understand different HTTP methods (GET, POST, PUT, DELETE, PATCH) and their use cases.
- [ ] Learn about HTTP status codes (200 OK, 201 Created, 400 Bad Request, 404 Not Found, 500 Internal Server Error).
- [ ] Design a simple entity for your MarketPlace Pro (e.g., `Product` with id, name, description, price).
    - [ ] Define this as a Java Record or a POJO.
- [ ] Create a new Spring Boot Controller (e.g., `ProductController`).
- [ ] Implement CRUD operations for the `Product` entity:
    - [ ] **POST** `/products` - Create a new product.
        - Takes product details in the request body.
        - Returns 201 Created with the created product (or its URI).
    - [ ] **GET** `/products/{id}` - Get a product by its ID.
        - Uses path variable for `id`.
        - Returns 200 OK with the product or 404 Not Found.
    - [ ] **GET** `/products` - Get all products.
        - Returns 200 OK with a list of products.
    - [ ] **PUT** `/products/{id}` - Update an existing product.
        - Takes product details in the request body.
        - Returns 200 OK with the updated product or 404 Not Found.
    - [ ] **DELETE** `/products/{id}` - Delete a product by its ID.
        - Returns 204 No Content on success or 404 Not Found.
- [ ] Use an in-memory collection (e.g., `List<Product>`) in the controller for now to store products (persistence will be added next).
- [ ] Test all endpoints using `curl` or Postman, verifying request bodies, responses, and status codes.

## 2. Introduction to Data Persistence with Spring Data JPA
- [ ] Research: What is JPA (Java Persistence API)? What is Spring Data JPA?
- [ ] Add Spring Data JPA dependency to `pom.xml` or `build.gradle`.
- [ ] Add an in-memory database dependency like H2 Database.
- [ ] Configure H2 database in `application.properties` (e.g., enable H2 console).
- [ ] Annotate your `Product` entity with JPA annotations (e.g., `@Entity`, `@Id`, `@GeneratedValue`).
- [ ] Create a Spring Data Repository interface for the `Product` entity (e.g., `ProductRepository extends JpaRepository<Product, Long>`).
- [ ] Refactor `ProductController` to use `ProductRepository` for CRUD operations instead of the in-memory list.
    - [ ] Autowire the `ProductRepository` into the controller.
- [ ] Test all CRUD endpoints again, verifying data is persisted in H2 (you can use H2 console accessible via browser, typically at `/h2-console`).

## 3. Basic Error Handling
- [ ] Implement basic error handling in the controller for scenarios like product not found.
- [ ] Use `@ResponseStatus` or `ResponseEntity` to return appropriate error codes.
- [ ] Research Spring's `@ControllerAdvice` and `@ExceptionHandler` for more global error handling (can be a stretch goal for this week).

## 4. Unit Testing Basics (Controllers)
- [ ] Add Spring Boot Test starter dependency if not already present.
- [ ] Write basic unit tests for `ProductController` using `@WebMvcTest`.
- [ ] Mock the `ProductRepository` using `@MockBean`.
- [ ] Test scenarios like:
    - Creating a product successfully.
    - Getting a product by ID when it exists.
    - Getting a product by ID when it does not exist (expect 404).
- [ ] Aim for testing controller logic, not the repository itself (that's for integration tests later).

## 5. Refine Project Structure
- [ ] Organize code into appropriate packages (e.g., `com.example.marketplacepro.controller`, `com.example.marketplacepro.model`, `com.example.marketplacepro.repository`).
- [ ] Ensure consistent naming conventions.
- [ ] Commit changes frequently with meaningful messages.
