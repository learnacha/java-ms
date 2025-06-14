# Week 01: Low-Level Requirements

## 1. Development Environment Setup
- [ ] Install Java 21+ (JDK)
- [ ] Verify Java installation ( `java -version` and `javac -version`)
- [ ] Choose and install an IDE (e.g., IntelliJ IDEA, Eclipse, VS Code with Java extensions)
- [ ] Configure IDE with the installed JDK
- [ ] Install Maven or Gradle (build tool)
- [ ] Verify build tool installation (e.g., `mvn -version` or `gradle -version`)
- [ ] Install Git for version control
- [ ] Verify Git installation (`git --version`)
- [ ] Set up a GitHub (or other Git provider) account if not already done
- [ ] Create a new Git repository for the "MarketPlace Pro" project (can be local for now)

## 2. Introduction to Spring Boot
- [ ] Research: What is Spring Boot? Key features and advantages.
- [ ] Go through Spring Boot official getting started guide (e.g., Building an Application with Spring Boot)
- [ ] Create a simple "Hello World" Spring Boot application using Spring Initializr (start.spring.io)
    - [ ] Select Java, Maven/Gradle, latest stable Spring Boot version
    - [ ] Add "Spring Web" dependency
- [ ] Import the generated project into the IDE
- [ ] Run the application and verify it starts correctly
- [ ] Create a simple REST controller that returns "Hello, MarketPlace Pro!" at an endpoint (e.g., `/hello`)
- [ ] Test the endpoint using a browser or a tool like `curl` or Postman.

## 3. Basic Project Structure
- [ ] Understand the default Spring Boot project structure (src/main/java, src/main/resources, src/test/java)
- [ ] Create a main application class (e.g., `MarketplaceProApplication.java`)
- [ ] Create a simple controller class (e.g., `HelloController.java`)
- [ ] Review `pom.xml` or `build.gradle` for dependencies.

## 4. Version Control Basics
- [ ] Initialize a Git repository in the project folder (if not done via IDE/Spring Initializr)
- [ ] Create a `.gitignore` file with common Java/IDE exclusions
- [ ] Make the first commit: "Initial commit - Spring Boot Hello World application"
- [ ] (Optional) Push the initial commit to a remote repository (e.g., GitHub)
