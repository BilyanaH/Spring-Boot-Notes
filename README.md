# Spring Boot Cheat Sheet

A concise, well-structured cheat sheet covering Spring Boot fundamentals, architecture, annotations, configuration, and common patterns.

Resources:

- [GeeksforGeeks: Spring Boot overview](https://www.geeksforgeeks.org/advance-java/spring-boot/)
- [Medium: Spring Boot Essentials (interview guide)](https://medium.com/@lakshyachampion/spring-boot-essentials-the-interview-cheat-sheet-e81ee59ce646)
- [Baeldung: Spring Boot guide](https://www.baeldung.com/spring-boot)
## Table of Contents

### Fundamentals
- [Spring](#spring)
- [Spring Boot](#spring-boot)
- [Spring MVC](#spring-mvc)

### Architecture & Configuration
- [Spring Boot Architecture](#spring-boot-architecture)
  - [Architecture Layers](#architecture-layers)
  - [Flow Architecture](#spring-boot-flow-architecture)

### Core Components
- [Annotations](#annotations)
- [Spring Boot Auto-Configuration](#spring-boot-auto-configuration)
- [Dispatcher Servlet in Spring](#what-is-dispatcher-servlet-in-spring)

### Dependency Injection & Beans
- [Spring Injection](#spring-injection)
- [Spring Autowiring](#spring-autowiring)
- [`@Autowired` and `@Qualifier`](#autowired-and-qualifier)
- [Circular Dependency](#circular-dependency)
- [BeanFactory vs ApplicationContext](#beanfactory-vs-applicationcontext-in-spring)
- [3 Ways to Create Spring Beans](#3-ways-to-create-spring-beans)
- [Bean Life Cycle](#bean-life-cycle)
- [Singleton and Prototype Scopes](#singleton-and-prototype-bean-scopes)
- [Custom Bean Scope](#custom-bean-scope)

### Build & Configuration
- [Introduction to Build Tools](#introduction-to-build-tools)
- [Dependency Management](#dependency-management)
- [Application Properties](#application-properties)
- [Profiling in Spring Boot](#profiling-in-spring-boot)
- [Actuator](#actuator)
- [DevTools](#devtools)

### REST & APIs
- [Introduction to RESTful Web Services](#introduction-to-restful-web-services)
- [REST Controller](#rest-controller)
- [JSON and Jackson](#json-and-jackson)
- [Spring Boot Exception Handling Architecture](#spring-boot-exception-handling-architecture)

 
# Spring
Spring is a comprehensive Java framework that provides support for building robust and scalable enterprise applications. It focuses on dependency injection, aspect-oriented programming, and modular architecture.

- **Dependency Injection (DI)**: Simplifies object creation and management, promoting loose coupling.
- **Modular Framework**: Offers various modules like Spring MVC, Spring Security, Spring Data, allowing selective use.
- **Flexible Configuration**: Supports XML, annotations, and Java-based configuration for application setup.

# Spring Boot 
Spring Boot is a project built on top of Spring that simplifies the development of Spring applications by providing auto-configuration, embedded servers, and production-ready features. It is designed to reduce boilerplate code and setup complexity.

- **Auto-Configuration**: Automatically configures Spring applications based on the dependencies added.
- **Embedded Servers**: Comes with embedded Tomcat, Jetty, or Undertow, eliminating the need for external servers.
- **Starter POMs**: Provides ready-to-use dependencies to simplify build configuration.

# Spring MVC
Spring MVC is a web framework module of the Spring Framework that helps in building web applications following the Model-View-Controller pattern. It provides full control over application architecture and is highly flexible.

- **Model-View-Controller (MVC) Pattern**: Separates application logic, UI, and request handling.
- **Flexible Configuration**: Supports XML, annotations, and Java-based configuration.
- **Integration**: Works with Spring modules like Spring Security, Spring Data, and Hibernate.


# Spring Boot Architecture
Spring Boot is a framework built on top of the Spring Framework that simplifies application development by providing auto-configuration, embedded servers, and production-ready features. Its architecture is designed to reduce boilerplate code, making it easier to build standalone, scalable, and maintainable Java applications.

- Follows layered and modular architecture for better scalability
- Includes starter dependencies to simplify dependency management
- Offers production-ready features like monitoring and health checks

## Architecture Layers
![Spring Boot Architecture Layers](https://media.geeksforgeeks.org/wp-content/uploads/20260112154010794308/presentationlayer.webp)

### 1. Presentation Layer
The Presentation Layer acts as the entry point of the Spring Boot application, also known as the controller layer. It is responsible for handling all incoming HTTP requests and sending appropriate responses back to the client.

Responsibilities
- Handles HTTP methods such as GET, POST, PUT, DELETE
- Exposes RESTful APIs using controllers
- Performs request validation
- Manages authentication entry points
- Converts Java objects to JSON and vice versa
- Forwards validated requests to the Business Layer

Common Components
- @RestController / @Controller
- @RequestMapping, @GetMapping, @PostMapping
- @RequestBody, @PathVariable

### 2. Business Layer
The Business Layer, also known as the Service Layer, contains the core business logic of the application. It acts as an intermediary between the Presentation and Persistence layers.

Responsibilities
- Implements business rules and workflows
- Processes and validates data
- Handles authentication and authorization logic (using Spring Security if required)
- Manages transactions using @Transactional
- Communicates with the Persistence Layer to retrieve or store data

Common Components
- @Service
- @Transactional

### 3. Persistence Layer
The Persistence Layer is responsible for database interaction and data access logic. It abstracts the underlying database operations from the rest of the application.

Responsibilities:
- Maps Java objects to database tables using ORM frameworks
- Performs CRUD (Create, Read, Update, Delete) operations
- Manages database transactions
- Supports both relational and NoSQL databases

Technologies Used
- Spring Data JPA
- Hibernate
- R2DBC (for reactive applications)

Common Components
- @Repository
- JpaRepository, CrudRepository
- @Entity, @Id, @Table
### 4. Database Layer
The Database Layer contains the actual database where the application data is stored. It can support:

- Relational Databases (MySQL, PostgreSQL, Oracle, SQL Server).
- NoSQL Databases (MongoDB, Cassandra, DynamoDB, Firebase).
- Cloud-based databases for scalability.

## Spring Boot Flow Architecture
![Spring Boot Flow Architecture](https://media.geeksforgeeks.org/wp-content/uploads/20250828113913303626/introduction-to-Spring-Boot.webp)
Let’s understand the layered architecture in application development, which helps organize code by separating responsibilities into different layers, improving maintainability and scalability.

- **Client Layer**: The external user or system that sends HTTP/- HTTPS requests to interact with the application.
- **Controller Layer (Presentation Layer)**: Handles client requests, processes them, and forwards them to the service layer while returning responses.
- **Service Layer (Business Logic Layer)**: Contains the business logic and coordinates operations between the controller and repository layers.
- **Repository Layer (Data Access Layer)**: Manages database operations such as create, read, update, and delete (CRUD).
- **Model Layer (Entity Layer)**: Represents the application's data structure and maps Java objects to database tables.
- **Database Layer**: The storage system where application data is permanently stored and retrieved.

# Annotations 
Annotations in Spring Boot are metadata that provide instructions to the Spring framework at runtime or compile time. Instead of using complex XML configurations, annotations allow developers to configure applications directly in Java code.

- Reduces XML-based configuration
- Improves code readability and maintainability
- Enables auto-configuration
- Simplifies dependency injection
- Speeds up application development
## Core Spring Boot Annotations

### 1. `@SpringBootApplication`

- This annotation is used to mark the main class of a Spring Boot application.
- It encapsulates `@SpringBootConfiguration`, `@EnableAutoConfiguration`, and `@ComponentScan` annotations with their default attributes.

```java
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

### 2. `@SpringBootConfiguration`
![SpringBootConfiguration](https://media.geeksforgeeks.org/wp-content/uploads/20240228162840/SpringBoot-Annotation.png)

Indicates that a class provides configuration for a Spring Boot application. It is a specialized version of `@Configuration` and is automatically included in `@SpringBootApplication`.

```java
@SpringBootConfiguration
public class AppConfig {
}
```

### 3. `@EnableAutoConfiguration`

Enables Spring Boot’s auto-configuration mechanism, automatically configuring beans based on classpath dependencies and application properties.

```java
@EnableAutoConfiguration
public class AppConfig {
}
```

### 4. `@ComponentScan`

Tells Spring where to search for components like `@Controller`, `@Service`, `@Repository`, etc.

```java
@ComponentScan("com.example")
public class AppConfig {
}
```

## Spring Bean Annotations

### 1. `@Component`

Marks a class as a generic Spring-managed component. Spring automatically detects and registers it during component scanning.

```java
@Component
public class EmailService {
}
```

### 2. `@Service`

Used in the service layer to define business logic and improve code readability.

```java
@Service
public class UserService {
}
```

### 3. `@Repository`

Used in the DAO(Data Access Object) layer to interact with the database. Automatically translates database-related exceptions into Spring exceptions.

```java
@Repository
public class UserRepository {
}
```

### 4. `@Configuration`

Indicates that a class contains Spring configuration and bean definitions. Acts as a replacement for XML-based configuration.

```java
@Configuration
public class AppConfig {
}
```

### 5. `@Bean`

Used to define a Spring bean explicitly inside a configuration class. Gives full control over bean creation and lifecycle.

```java
@Configuration
public class AppConfig {
    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

## Dependency Injection Annotations

### 1. `@Autowired`

Automatically injects required dependencies into a class. Eliminates the need for manual object creation.

```java
@Autowired
private UserService userService;
```

### 2. `@Qualifier`

Specifies which bean to inject when multiple beans of the same type exist.

```java
@Autowired
@Qualifier("emailService")
private NotificationService service;
```

### 3. `@Primary`

Marks a bean as the default choice among multiple candidates. Used when no `@Qualifier` is explicitly specified.

```java
@Primary
@Component
public class SmsService implements NotificationService {
}
```

## Web and REST API Annotations

### 1. `@RestController`

Used to create RESTful web services and automatically returns data in JSON or XML format.

```java
@RestController
public class HelloController {
}
```

### 2. `@RequestMapping`

Maps HTTP requests to controller classes or methods. Defines the base URL path for request handling.

```java
@RequestMapping("/api")
public class ApiController {
}
```

### 3. HTTP Method Annotations

| Annotation | HTTP Method | Explanation |
| --- | --- | --- |
| `@GetMapping` | GET | Retrieves data from the server |
| `@PostMapping` | POST | Sends data to the server |
| `@PutMapping` | PUT | Updates existing data |
| `@DeleteMapping` | DELETE | Deletes data |

Example:

```java
@GetMapping("/users")
public List<User> getUsers() {
    return userService.getAllUsers();
}
```

### 4. `@PathVariable`

Extracts values from the URI path and binds them to method parameters.

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable int id) {
    return userService.getUser(id);
}
```

### 5. `@RequestParam`

Reads query parameters from the request URL. Used for optional or filtering inputs.

```java
@GetMapping("/search")
public String search(@RequestParam String keyword) {
    return keyword;
}
```

### 6. `@RequestBody`

Binds the HTTP request body to a Java object. Commonly used with POST and PUT requests.

```java
@PostMapping("/users")
public User saveUser(@RequestBody User user) {
    return userService.save(user);
}
```

## Configuration and Properties Annotations

### 1. `@Value`

Injects individual property values from `application.properties` or `application.yml`.

```java
@Value("${server.port}")
private String port;
```

### 2. `@ConfigurationProperties`

Binds a group of related configuration properties to a POJO(Plain Old Java Object) in a type-safe manner. 

properties:
``` properties
app.name=TheatreManager
app.version=1.0
app.timeout=5000
```

```java
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
    private String version; 
    private int timeout;
}
```

## Conditional Annotations

### `@ConditionalOnProperty`

`@ConditionalOnProperty` is a Spring Boot annotation 

- Allows conditional bean creation based on property values
- Useful for feature toggles and environment-specific configurations
- Prevents bean instantiation if the property condition is not met

```java
@Configuration
public class MyConfig {
  
    @Bean
    @ConditionalOnProperty(prefix = "feature", name = "enabled", havingValue = "true")
    public MyService myService() {
        return new MyService();
    }
}
```

**Explanation:** If `feature.enabled=true` is set in `application.properties`, the `myService` bean will be created. If `feature.enabled=false` or the property is missing, the bean will not be created.

## Validation Annotations


Validating user input is essential for building secure and reliable applications. Spring Boot simplifies validation by using Hibernate Validator, allowing developers to apply rules using simple annotations.

- **Ensures data integrity and prevents invalid input.**
- **Uses annotations** like `@NotNull`, `@Size`, and `@Email` to declare constraints on fields.
- **Improves application security and reliability.**

Common Hibernate Validator annotations:

- `@NotNull` — Ensures a field is not null (empty strings or collections are allowed).
- `@NotEmpty` — Ensures a field is not null and not empty (strings/collections must contain at least one element/character).
- `@NotBlank` — Applies only to strings; ensures not null, not empty, and contains at least one non-whitespace character.
- `@Min` — Validates that a numeric value is greater than or equal to the specified minimum.
- `@Max` — Validates that a numeric value is less than or equal to the specified maximum.
- `@Size` — Validates the size of a collection, array, map, or string (min/max length).
- `@Email` — Validates that the annotated string is a well-formed email address.
- `@Pattern` — Validates that the string matches the provided regular expression.

Usage note: apply validation on controller input using `@Valid` (or `@Validated`) on request bodies or method parameters; handle validation failures with a `BindingResult` or a global `@ControllerAdvice` catching `MethodArgumentNotValidException` to return user-friendly error responses.

Example:

```java
public class User {
    @NotBlank
    private String name;

    @Email
    private String email;

    @Min(18)
    private int age;
}

@RestController
public class UserController {
    @PostMapping("/users")
    public ResponseEntity<?> createUser(@Valid @RequestBody User user, BindingResult br) {
        if (br.hasErrors()) {
            return ResponseEntity.badRequest().body(br.getAllErrors());
        }
        return ResponseEntity.ok(user);
    }
}
```

## Exception Handling Annotations

### 1. `@ExceptionHandler`

Handles specific exceptions within a controller. Allows custom error responses for exceptions.

```java
@ExceptionHandler(Exception.class)
public String handleException() {
    return "Error occurred";
}
```

### 2. `@ControllerAdvice`

Provides global exception handling across all controllers. Centralizes error-handling logic.

```java
@ControllerAdvice
public class GlobalExceptionHandler {
}
```

## JPA and Database Annotations

| Annotation | Purpose |
| --- | --- |
| `@Entity` | Marks a class as a JPA entity |
| `@Table` | Specifies table mapping |
| `@Id` | Defines primary key |
| `@GeneratedValue` | Auto-generates primary key values |
| `@Column` | Maps class field to table column |


# Spring Boot Auto-Configuration
Spring Boot's auto-configuration automatically configures application components based on the dependencies present on the classpath and sensible defaults. Enabled via `@EnableAutoConfiguration` (included in `@SpringBootApplication`), it creates and wires common beans and infrastructure so developers can focus on business logic instead of boilerplate setup.

Example — if the `spring-boot-starter-web` dependency is present, Spring Boot auto-configures an embedded web server and sets up the `DispatcherServlet`, reducing configuration overhead.

## Why Auto-Configuration is Important
Before Spring Boot, developers had to manually configure many components in Spring applications.

Common manual tasks included:
- Configuring `DispatcherServlet`
- Configuring view resolvers
- Configuring database connections
- Configuring transaction management
- Configuring embedded servers

Spring Boot solves this problem using Auto-Configuration.

## How Auto-Configuration Works
Auto-configuration works using the `@EnableAutoConfiguration` annotation. This annotation tells Spring Boot to automatically configure beans based on:

- Dependencies in the classpath
- Application properties
- Existing beans in the application context

![SpringBootApplication](https://media.geeksforgeeks.org/wp-content/uploads/20260307155317759437/Auto.webp)
In most applications, developers use `@SpringBootApplication`, which internally includes:

```java
@Configuration
@EnableAutoConfiguration
@ComponentScan
```

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```
So when the application starts, Spring Boot scans the classpath and configures the required beans automatically.

## Steps to Implement Auto-Configuration in a Spring Boot Application

### 1. Create a Spring Boot Project
Use Spring Initializr and configure the project with the following settings:

- Project: Maven
- Language: Java
- Spring Boot Version: Latest stable version
- Group: com.example
- Artifact: auto-config-demo
- Packaging: Jar
- Java Version: 17 or later

Add the following dependency:

- Spring Boot Starter Web

This dependency automatically includes:

- Apache Tomcat (embedded server)
- Spring Web MVC
- JSON support

### 2. Main Application Class
The main class contains the `@SpringBootApplication` annotation which enables auto-configuration.

```java
@SpringBootApplication
public class AutoConfigDemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(AutoConfigDemoApplication.class, args);
    }
}
```

### 3. Create a Controller
Create a controller class inside the same package.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello Spring Boot Auto Configuration";
    }
}
```

### 4. Run and Test the Application
Run the main class `AutoConfigDemoApplication` and visit:

`http://localhost:8080/hello`

Spring Boot automatically performs the following configurations:
- Starts embedded Apache Tomcat
- Configures `DispatcherServlet`
- Enables Spring Web MVC
- Configures request mapping and JSON converters

You do not need to manually configure:
- Web server
- Servlet configuration
- MVC configuration

# What is Dispatcher Servlet in Spring?
The **Dispatcher Servlet** is the "Front Controller" of a Spring Web application. It acts as the single entry point for every HTTP request coming into your app.

The Dispatcher Servlet is the front controller in the Spring MVC framework. It is a core component that handles all incoming HTTP requests and routes them to the appropriate handlers (controllers). Acting as the central point of the Spring MVC architecture, it manages the entire request-response lifecycle.

Key responsibilities:
- Receive every HTTP request and act as the single entry point for the web layer.
- Consult `HandlerMapping` to determine the correct controller (handler) for a request.
- Dispatch the request to the resolved handler and invoke the handler adapter.
- Coordinate request processing, view resolution, and response rendering.

Example flow:
1. Request arrives at the `DispatcherServlet`.
2. `HandlerMapping` finds the appropriate controller method.
3. The controller executes business logic and returns a `ModelAndView` (or body).
4. `ViewResolver` is used to resolve and render the view (for web pages) or message converters serialize the response (for REST).

# Spring Injection
Spring Dependency Injection (DI) is a fundamental concept in the Spring Framework that allows objects to receive their dependencies from an external source rather than creating them internally.

- Eliminates the need for classes to create their own dependencies
- Makes code more reusable and modular
- Supports constructor, setter, and field injection
- Works with XML configuration, annotations, or Java-based configuration
![Spring Dependency Injection](https://media.geeksforgeeks.org/wp-content/uploads/20260430123859420053/file.webp)
In above Diagram:

- The IoC (Inversion of Control) Container is responsible for creating and managing objects (called Beans).
- Bean 1 and Bean 2 are created by the container instead of being manually instantiated.
- If Bean 1 depends on Bean 2, the container automatically injects Bean 2 into Bean 1 (this is Dependency Injection).
- The configuration for this process is defined using XML or Java Annotations.

# Spring Autowiring 

**Autowiring** allows the Spring container to resolve and inject collaborating beans into your bean automatically, significantly reducing the need for manual configuration.

## 1. Autowiring Modes (XML Legacy)

While mostly replaced by annotations, these modes define the "logic" Spring uses to find a match:

| Mode | Strategy | Key Requirement |
| --- | --- | --- |
| **no** | No autowiring | Manual `<property>` tags in XML. |
| **byName** | Matches property name with Bean ID | Setter method required. |
| **byType** | Matches property type with Bean Class | Fails if >1 bean of same type exists. |
| **constructor** | Similar to `byType` but for constructors | Matches constructor arguments. |

---

## 2. Modern Autowiring: `@Autowired`

In Spring Boot and modern Spring (2026), we use the `@Autowired` annotation. It primarily works **byType**.

### **Field Injection:** 
Not recommended
```java
@Autowired
private State state;

```


### **Setter Injection:**
```java
@Autowired
public void setState(State state) { this.state = state; }

```


### **Constructor Injection:** (**Best Practice**)
```java
private final State state;
public City(State state) { this.state = state; }

```


## 3. Handling Ambiguity: `@Qualifier`

If you have **two beans of the same type** (e.g., two different `State` beans), `@Autowired` by itself will fail. You must use `@Qualifier` to specify which one to use.

```java
@Autowired
@Qualifier("sofiaState") // Tells Spring exactly which bean ID to inject
private State state;

```

---

## Summary of Pros & Cons

**Pros:**

* **Less Code:** No need for manual wiring in XML or Config classes.
* **Maintenance:** Adding a dependency is as simple as adding a parameter to a constructor.

**Cons:**

* **Hidden Dependencies:** It’s not always obvious which bean is being injected where just by looking at the class.
* **Ambiguity:** Requires extra care (`@Qualifier`) when multiple beans of the same type exist.

This is an excellent summary of how Spring handles bean ambiguity. For your notes, I have condensed the most important points into a clear, "ready-to-file" format.

---

# Circular Dependency
Circular dependency occurs when two or more beans in a Spring application depend on each other, either directly or indirectly, creating a loop. For example: Bean A depends on Bean B, and Bean B depends on Bean A. This prevents Spring from fully constructing either bean during startup.

How to resolve / avoid circular dependencies:

- Mark one of the dependencies as `@Lazy` to delay its initialization until it is actually needed.
- Replace constructor injection with setter (or field) injection for one of the beans so Spring can create the bean instance first and inject the dependency later.

Example:

```java
@Component
public class A {
    private final B b;

    public A(B b) { this.b = b; }
}

@Component
public class B {
    private A a;

    @Autowired
    public void setA(A a) { this.a = a; }
}
```

Using `@Lazy` on one dependency is another quick fix:

```java
@Component
public class A {
    private final B b;

    public A(@Lazy B b) { this.b = b; }
}
```

# `@Autowired` and `@Qualifier`

In Spring, **Dependency Injection (DI)** is the process where the container provides the objects (beans) a class needs to function, rather than the class creating them itself.

## 1. `@Autowired` (The Automatic Link)

The `@Autowired` annotation tells Spring: *"Find a bean of this **type** and inject it here."*

* **How it works:** It searches the application context for a matching class type.
* **Where to use:** Constructors (best practice), Setters, or Fields.
* **The Limitation:** If you have **two** beans of the same type (e.g., `SqlRepository` and `MongoRepository`, both implementing `MyRepository`), Spring won't know which one to pick and will throw a `NoUniqueBeanDefinitionException`.

## 2. `@Qualifier` (The Disambiguator)

The `@Qualifier` annotation is used **alongside** `@Autowired` to resolve ambiguity by specifying the exact **name** of the bean you want.

* **How it works:** It tells Spring: *"I know there are multiple beans of this type, but I specifically want the one named 'X'."*
* **Example (Constructor Injection):**
```java
public MyService(@Qualifier("mongoRepo") MyRepository repository) {
    this.repository = repository;
}

```


## Comparison Table

| Feature | `@Autowired` | `@Qualifier` |
| --- | --- | --- |
| **Main Goal** | Inject by **Type**. | Inject by **Name**. |
| **Ambiguity** | Causes an error if multiple beans exist. | Resolves errors by picking a specific bean. |
| **Flexibility** | High (automatic). | Granular (manual control). |
| **Best Practice** | Use for single-implementation services. | Use for multiple implementations of one interface. |

---

## `@Primary` vs `@Qualifier`

* **`@Primary`**: Use this on a bean class to say: *"If there are multiple beans, use this one by default unless a `@Qualifier` says otherwise."*
* **`@Qualifier`**: Always takes precedence over `@Primary`. It is more specific.

# BeanFactory vs ApplicationContext in Spring
![BeanFactory vs ApplicationContext in Spring](https://media.geeksforgeeks.org/wp-content/uploads/20260227111947198575/DifferenceBetweenBeanFactory-andApplicationContext.webp)

**BeanFactory**, defined in org.springframework.beans.factory, is the basic IoC container in Spring. It provides core functionalities such as bean creation and dependency injection.

- Beans are created only when requested
- This behavior is known as lazy initialization
- Suitable for lightweight or memory-constrained applications

**ApplicationContext**, defined in org.springframework.context, is an advanced container that extends BeanFactory and provides additional enterprise-level features.

- Eager initialization (by default)
- Annotation-based configuration
- Event handling
- Internationalization (i18n)
- Automatic post-processor registration


# 3 Ways to Create Spring Beans
![Ways to Create Spring Beans](https://media.geeksforgeeks.org/wp-content/uploads/20260228144635384648/different_methods_to_create_a_spring_bean.webp)
Spring Beans are objects managed by the **IoC (Inversion of Control) Container**, which handles their creation, configuration, and lifecycle.

### 1. XML Configuration (Legacy)

The traditional way to define beans in an external `beans.xml` file.

* **How:** Use the `<bean id="..." class="..." />` tag.
* **Pros:** Decouples configuration from Java code; no recompilation needed for config changes.
* **Cons:** Hard to maintain in large projects; no compile-time check.

### 2. Annotation-Based (Modern Standard)

The fastest way, widely used in **Spring Boot**. Spring "scans" your packages and finds beans automatically.

* **How:** 1. Mark classes with **`@Component`** (or `@Service`, `@Repository`).
2. Use **`@ComponentScan`** in a configuration class to tell Spring where to look.
* **Pros:** Minimal code; very easy to read and maintain.

### 3. Java-Based Configuration (Flexible & Typesafe)

Explicitly defining beans using a Java class.

* **How:** 1. Mark a class with **`@Configuration`**.
2. Create methods returning an object and mark them with **`@Bean`**.
* **Pros:** **Type-safe** (compiler catches errors); perfect for configuring 3rd-party libraries where you can't add `@Component`.

---

### Quick Comparison Table

| Method | Key Tool | Best Use Case |
| --- | --- | --- |
| **XML** | `<bean>` tag | Legacy systems / Externalized config. |
| **Annotation** | `@Component` | Your own classes in Spring Boot. |
| **Java Config** | `@Bean` | External libraries / Complex bean logic. |

---

## 1. How It Works (The Workflow)
![Dispatcher Servlet](https://media.geeksforgeeks.org/wp-content/uploads/20260228113317618539/spring_mvc_architecture.webp)
Instead of having multiple servlets, everything goes through the Dispatcher Servlet, which coordinates the work:

1. **Request Arrival:** The client sends an HTTP request (e.g., `GET /api/details`).
2. **Handler Mapping:** The Dispatcher Servlet asks: *"Who handles this URL?"* It finds the matching Controller method (via `@GetMapping`, etc.).
3. **Controller Execution:** The Controller processes the business logic and returns data (Model) and a View name (or just the data for REST APIs).
4. **View Resolver:** (For Web pages) It finds the physical file (like a Thymeleaf template or JSP).
5. **Response:** The final result is sent back to the client.

---

### 2. Spring MVC vs. Spring Boot Setup

| Feature | **Traditional Spring MVC** | **Modern Spring Boot** |
| --- | --- | --- |
| **Configuration** | Manual setup in `web.xml`. | **Auto-configured.** Just add `spring-boot-starter-web`. |
| **Server** | Requires external Tomcat installation. | **Embedded Tomcat** (starts with the app). |
| **Registration** | Complex XML tags. | Automatic, or via a simple `@Bean` if customization is needed. |

---

### 3. Key Annotations to Remember

When the Dispatcher Servlet routes requests, it looks for these annotations in your classes:

* **`@RestController`**: Tells the Dispatcher Servlet that this class handles web requests and returns data directly (JSON/XML) instead of a HTML view.
* **`@RequestMapping("/path")`**: The base URL for the controller.
* **`@GetMapping`, `@PostMapping`, etc.**: Specific HTTP methods.
* **`@RequestBody`**: Tells the Servlet to convert the incoming JSON into a Java object.
* **`@PathVariable`**: Extracts values directly from the URL (e.g., `/api/details/{id}`).

---

### 4. Why use a Front Controller?

* **Centralized Control:** You can handle security, logging, and internationalization in one place before it reaches the controllers.
* **Looser Coupling:** Controllers don't need to know about the Servlet API or how the request was routed; they just focus on business logic.

---

# Bean Life Cycle
![Bean Life Cycle](https://media.geeksforgeeks.org/wp-content/uploads/20260227122521018332/container_started.webp)

## Container Initialization
- The Spring IoC container starts and loads configuration metadata (XML, annotations, or Java config).
- Bean definitions are registered, and infrastructure components (like processors) are prepared.
## Bean Instantiation
- The container creates the bean object using a constructor or factory method.
- At this stage, the bean exists in memory but dependencies are not yet injected.
## Dependency Injection
- The container resolves required dependencies from the IoC container.
- Dependencies are injected via constructor, setter, or field injection.
## Custom Init Method
- The custom init() method is called once all dependencies are injected.
- It is used to perform additional setup like initializing resources, validating properties, or starting connections.
## Custom Utility Method
- A Custom Utility Method is a normal business or helper method defined inside a Spring bean.
- The developer must manually call it through the bean reference.
## Destruction
- Cleanup logic is executed using @PreDestroy, destroy(), or custom destroy methods.
- Resources such as database connections or threads are released before bean removal.

_Note: Custom method names can be used instead of default lifecycle method names._

## Ways to Implement Bean Life Cycle in Spring
Spring provides three standard ways to manage the bean life cycle:
- XML Configuration
- Programmatic Approach (Interfaces)
- Annotations

# Singleton and Prototype Bean Scopes
## Bean Scopes (Built-in)
Spring defines several built-in bean scopes that control bean lifecycle and visibility. Use `@Scope("...")` (or web-aware scope constants) to declare a scope.

### Singleton (default)
- Instance: single shared instance per Spring IoC container.
- Created: when the `ApplicationContext` is initialized (eager by default).
- Destroyed: when the container shuts down.
- Container lifecycle management: fully managed (init + destroy callbacks supported).
- Typical use: stateless services, repositories, controllers.

### Prototype
- Instance: a new instance is created on each request to the container (e.g., each `getBean()` call).
- Created: on demand, when requested.
- Destroyed: not managed by the container (no callback lifecycle after creation).
- Initialization: lazy (created only when needed).
- Typical use: stateful or short-lived objects where each consumer needs its own instance.

### Request (web)
- Instance: one per HTTP request.
- Created: at the start of the HTTP request.
- Destroyed: at the end of the HTTP request.
- Scope requirements: web-aware context (e.g., `WebApplicationContext`).
- Typical use: request-scoped data such as request-specific holders or validators.

### Session (web)
- Instance: one per HTTP session.
- Created: on first request that requires the bean within a session.
- Destroyed: when the HTTP session is invalidated or times out.
- Typical use: per-user session data (shopping cart, user preferences).

### Application (web)
- Instance: one per web application (per `ServletContext`).
- Created: when the web application starts (or when first requested depending on configuration).
- Destroyed: when the web application is stopped.
- Shared across all requests and sessions.
- Typical use: application-wide resources that must be shared across the whole app.

Examples:
- Declare prototype: `@Scope("prototype")`
- Request scope (Spring Web): `@Scope(value = WebApplicationContext.SCOPE_REQUEST)`


# Custom Bean Scope
In the Spring Framework, bean scopes define the lifecycle and visibility of beans within the application context. Spring provides several built-in scopes such as singleton, prototype, request, session, and application. However, some applications require more control over bean lifecycle, which can be achieved using custom bean scopes.

- Spring allows developers to create custom bean scopes when built-in scopes do not meet application needs.
- Custom scopes help control bean creation and destruction based on specific business logic.
- They provide greater flexibility in managing bean lifecycle in complex applications.
## When to Use Custom Scopes
- When a bean needs to live beyond a single HTTP request but less than a singleton.
- When managing resources per thread, user, or tenant.
- When the built-in scopes do not provide the required lifecycle behavior.

## How to do it? 
### 1. Implement the `Scope` Interface

To define how your beans should be created, stored, and retrieved, you must implement the `org.springframework.beans.factory.config.Scope` interface.

This interface requires you to define several key methods:

* **`get(String name, ObjectFactory<?> objectFactory)`**: Returns the bean from the underlying scope or creates it using the factory if it doesn't exist.
* **`remove(String name)`**: Removes the object from the underlying scope.
* **`registerDestructionCallback(String name, Runnable callback)`**: Defines a callback to be executed when the scope is destroyed or the object is removed.
* **`getConversationId()`**: Returns an identifier for the current context (e.g., the Thread name or a Session ID).

### 2. Register the Custom Scope

Once the implementation is ready, Spring needs to be informed about the new scope. You do this by registering it in your configuration using the `CustomScopeConfigurer`.

**Key steps for registration:**

* **Create a `CustomScopeConfigurer` Bean**: This is a special Spring bean that helps register custom scopes during the container startup.
* **Map a Name**: Assign a unique String name (e.g., `"thread-local"` or `"tenant-scope"`) to your scope implementation instance.

```java
@Bean
public static CustomScopeConfigurer customScopeConfigurer() {
    CustomScopeConfigurer configurer = new CustomScopeConfigurer();
    Map<String, Object> scopes = new HashMap<>();
    scopes.put("my-custom-scope", new MyCustomScopeImplementation());
    configurer.setScopes(scopes);
    return configurer;
}

```

### 3. Apply the Scope to a Bean
After registration, you can use your custom scope just like the built-in ones by using the `@Scope` annotation on your components or bean definitions:

```java
@Bean
@Scope("my-custom-scope")
public MyService myService() {
    return new MyService();
}

```
**Why use this?**

* **Thread Isolation:** Ensuring each thread has its own instance of a bean (Thread-Local).
* **Resource Management:** Limiting bean lifespan to specific business logic segments.
* **Flexibility:** Precise control over the "where" and "how long" of a bean's existence in memory.

# Introduction to Build Tools
## Anatomy of a Build: The Dependency Graph
The anatomy of a build is based on a dependency graph, usually a **Directed Acyclic Graph (DAG)**, which maps how modules depend on each other. The build tool uses this graph to determine the correct order of operations, ensuring that dependencies are built before the modules that rely on them. This approach optimizes build time and avoids unnecessary work.

- Parallel Execution – Independent modules can be built simultaneously, reducing total build time.
- Incremental Builds – Only modules that have changed or depend on changed files are rebuilt.
- Dependency Ordering – Ensures that modules are built in the correct sequence to avoid errors.
> Build tools help developers automate compilation, manage dependencies, and streamline workflows across projects. They save time, reduce errors, and improve efficiency.

![Top 5 build tools](https://media.geeksforgeeks.org/wp-content/uploads/20250804154950120020/top_5_build_tools.webp)

## Apache Maven
- Philosophy: "Convention over Configuration." It enforces a standard directory structure (src/main/java).
- Config: Uses pom.xml (XML).
- Pros: Extremely stable, massive plugin ecosystem.
- Cons: XML is verbose; rigid structure.

### Maven Default Build Lifecycle
Maven provides a default build lifecycle composed of ordered phases. Running a specific phase executes that phase and all earlier phases.

- `validate`: Validates the project structure and ensures all required information is available.
- `compile`: Compiles the project's source code.
- `test`: Runs unit tests (e.g., JUnit or TestNG).
- `package`: Packages compiled code into distributables (JAR/WAR).
- `verify`: Runs checks to ensure the package meets quality criteria.
- `install`: Installs the package into the local Maven repository for use as a dependency.
- `deploy`: Deploys the packaged artifact to a remote repository for sharing.

Example: running `mvn package` executes `validate`, `compile`, `test`, then `package`.

## Gradle
- Philosophy: Flexibility and Performance. Uses a Domain Specific Language (DSL).
- Config: Uses build.gradle (Groovy or Kotlin).
- Pros: Highly customizable, faster (incremental builds), standard for Android.
- Cons: Steeper learning curve.


# Dependency Management
## Importance of Dependency Management

- Centralized Dependency Management: All dependencies are managed in one place, typically in the pom.xml (for Maven) or build.gradle (for Gradle) file.
- Automatic Version Management: When we change the Spring Boot version, the versions of all related dependencies are automatically updated.
- Conflict Prevention: It helps prevent version conflicts between different libraries, especially in multi-module projects.

Note: Dependency Management is a way of managing all the required dependencies in one place and efficiently making use of them.

## Life Cycle of Dependency Management

The below diagram demonstrates the type of Dependency Management

![Dependency-Management life-cycle](https://media.geeksforgeeks.org/wp-content/uploads/20250312160622555937/Dependency-Management.webp)

## Working of Dependency Management in Spring-Boot

- Dependency is nothing but a 'Library' that provides specific functionality that we can use in our application.
- In Spring-Boot, Dependency Management and Auto-Configuration work simultaneously.
- It is the auto-configuration that makes managing dependencies supremely easy for us.
- We have to add the dependencies in the pom.xml/build.gradle file.
- These added dependencies will then get downloaded from Maven Central.
- The downloaded dependencies will get stored into the '.m2' folder in the local file system.
- The Spring-Boot application can access these dependencies from  '.m2' and its sub-directories.

![MVNRepository](https://media.geeksforgeeks.org/wp-content/uploads/20250312145914400660/MVNRepository.png)

## Project Build Systems

Spring Boot supports two main build system Maven and Gradle.

- Maven: Dependencies are managed in the pom.xml file.
- Gradle: Dependencies are managed in the build.gradle file.

Maven and Gradle use a different syntax for managing dependencies.
Also, we don't need to mention the version of the dependencies, as Spring-Boot configures them automatically. Though we can mention the version or override as well.

## Key features of Maven build

- It uses the default Java compiler.
- It has UTF-8 source encoding
- A useful feature of not mentioning the version information of dependencies is inherited from POM ( spring-boot-dependencies ).
- Resource filtering and plugin configurations.
- Resource filtering is also for 'application.properties' and 'application.yml'.

## Spring-Boot Starters

Spring Boot Starters are a set of convenient dependency descriptors provided by Spring Boot that simplify the setup of your application by grouping commonly used libraries and configurations into a single, reusable module.

_Example: 'spring-boot-starter-jdbc'_

## Types of Starters

- Application Starters: For building specific types of applications (e.g., spring-boot-starter-web).
- Technical Starters: For technical features like logging or security (e.g., spring-boot-starter-security).
- Production-ready Starters: For monitoring and managing production applications (e.g., spring-boot-starter-actuator).

All the required dependencies of Spring-Boot are embedded in the 'dependencies' tag/block.

Maven -> pom.xml

```xml
<dependencies>
     <dependency>
          <groupId> ... </groupId>
          <artifactId> ... </artifactId>
          <version> ... </version>
     </dependency>
</dependencies>
```

## Adding Dependencies in Spring Boot

### 1. Using Maven (pom.xml)

I
If we know the dependency, we can directly place them in the pom.xml file. For example to add the Thymeleaf template engine in your project build, one can add the following dependency in the `<dependencies></dependencies>` tag.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

pom.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.4.3</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <groupId>sia</groupId>
    <artifactId>GFG</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>GFG</name>
    <description>GFG Application</description>

    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Spring Boot Starter Web for building web applications -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- Spring Boot Starter Thymeleaf for rendering views -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>

        <!-- Lombok for reducing boilerplate code -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- Spring Boot Starter Test for unit testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <!-- Spring Boot DevTools for enhanced development experience -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- Spring Boot Maven Plugin for packaging the application -->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <!-- Exclude Lombok from the packaged application -->
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

#### Understanding/Configuring Dependencies
Starter Parent: To take advantage of auto-configured 'sensible' defaults, we should add Starter Parent in the project.
```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>___</version>
</parent>
```
With default configuration like above, we can override respective dependencies by overriding a 'property'.

```xml
<properties>
    <slf4j.version>___</slf4j.version>
</properties>
```

This will make sure that the mentioned version of a SLf4j library will be used.
We can also manage auto-configured 'Starter Parent' and create a custom POM without the need to specify the first one with the help of artifact 'scope=import' of 'spring-boot-dependencies'.

```xml
 <dependencyManagement>
     <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>___</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

After this, we can normally add the dependencies like the one mentioned above. But, to override the individual dependency, we need to add a respective entry before the 'spring-boot-dependencies' entry.

```xml
<dependencyManagement>
    <dependencies>

        <!-- Override SLF4J provided by Spring Boot -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>___</version>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>___</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>

    </dependencies>
</dependencyManagement>
```

But, we have to manually configure the plugin management by adding 'spring-boot-maven-plugin' explicitly. Managing the Maven plug-in is very essential as it packs the Spring-Boot application into an executable jar.

Maven -> pom.xml

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

Java Version: We can also change the java version in the following:

```xml
<properties>
    <java.version>___</java.version>
</properties>
```

Developer Tools: A set of specific tools to make the application development process much easier. It is in the 'spring-boot-devtools' module.

Maven -> pom.xml

```xml
<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-devtools</artifactId>
     <optional>true</optional>
</dependency>
```

### 2. Using Gradle

In the case of a 'Starter Parent' like in Maven, here there is no 'Super Parent' to take advantage of some auto configurations. To add dependencies in Gradle, add them in the 'dependencies{ }' section. For providing executable jar, we can add the following in the dependencies section

'spring-boot-gradle-plugin'

build.gradle:

```gradle
buildscript {
    repositories {
        mavenCentral() // Use Maven Central instead of jcenter (jcenter is deprecated)
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:3.4.4") 
    }
}
apply plugin: 'java'
apply plugin: 'org.springframework.boot' 
repositories {
    mavenCentral() // Use Maven Central for dependencies
}
dependencies {
    implementation("org.springframework.boot:spring-boot-starter-web") 
    testImplementation("org.springframework.boot:spring-boot-starter-test") 
}
```

For adding the 'Developer tools', add the following in the 'dependencies' block

Gradle -> build.gradle

```gradle
developmentOnly("org.springframework.boot:spring-boot-devtools")
```

_Note: Each release of Spring Boot is associated with a base version of the Spring Framework, so it is highly recommended to not specify its version on your own._

# Application Properties

In Spring Boot applications, configuration is important for customizing application behavior without modifying the source code. Spring Boot allows developers to manage settings using configuration files like application.properties or application.yml.

- These files help define settings such as server port, database configuration, and logging levels.
- They make the application easier to maintain and allow different configurations for different environments.

## Why Use application.properties?
- Centralized configuration management.
- Easy to override default Spring Boot settings.
- Provides flexibility for different environments (dev, test, prod).
- Reduces hardcoding in source code.

## Commonly Used Properties
### 1. Server Configuration
We can change the default port (8080) of a Spring Boot application by setting the property server.port in the application.properties file. 

``` properties
server.port=8989
```

### 2. Defining the Application Name
We can set a custom name for your Spring Boot application using the spring.application.name property in the application.properties.

``` properties
string.application.name=TheatreManager
```
### 3. Database Configuration
To connect your Spring Boot application with a database, specify the required properties such as spring.datasource.url, spring.datasource.username and spring.datasource.password in the application.properties file. These properties vary depending on the database (e.g., MySQL, PostgreSQL, Oracle).

**MySQL Configuration (.properties)**
``` properties
spring.datasource.url=jdbc:mysql://localhost:3306/theatre_db
spring.datasource.username=root
spring.datasource.password=secret
spring.jpa.hibernate.ddl-auto=update
```

### 4. Connecting with an Eureka Server
Eureka Server acts as a service registry in microservices architecture. Each microservice registers itself to Eureka, which maintains service discovery details.

## Using application.yml Instead of application.properties
The application.properties file is not very readable when dealing with complex configurations. Most developers prefer using application.yml (YAML format) instead. YAML is a superset of JSON and provides a more structured and readable way to define hierarchical configuration data. Let's convert some of the previous examples into YAML format.

``` yaml
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
  instance:
    prefer-ip-address: true
```
YAML configuration files allow developers to organize settings in a hierarchical and readable format.

## Why Use application.yml?
- Provides a structured and hierarchical configuration format.
- More readable for complex configurations.
- Reduces repetition compared to application.properties.
- Widely used in microservices and cloud-based Spring Boot applications.

## application.yml vs application.properties
Here is the cleaned and formatted comparison table for your cheat sheet, summarizing the key differences between the two configuration formats.

---

### **Comparison: `.properties` vs. `.yml`**

| Feature | **application.properties** | **application.yml** |
| --- | --- | --- |
| **Format** | Key-value pairs | Hierarchical structure |
| **Readability** | Less readable for large/complex configs | More readable |
| **Structure** | Flat structure | Nested/Tree-like structure |
| **Usage** | Best for simple, straightforward settings | Best for complex, multi-level configurations |

# Profiling in Spring Boot

Profiling in Spring Boot refers to the use of profiles to manage environment-specific configurations and beans. It allows you to define different configurations (e.g., for dev, test, prod) and activate them based on the environment. This makes your application flexible and easier to maintain across different deployment scenarios.

- Profiles allow environment-specific bean creation and property configuration
- Activated using the `spring.profiles.active` property
- Uses `@Profile` annotation to load beans or configurations specific to a profile
- Enables separate configurations for development, testing, and production environments

## Profile-Specific Configuration Files

You can create separate `application.properties` or `application.yml` files for each profile:

- `application.properties` — Common properties for all environments
- `application-dev.properties` — Development environment configuration
- `application-prod.properties` — Production environment configuration
- `application-test.properties` — Testing environment configuration

Spring Boot automatically loads the appropriate file based on the active profile set via `spring.profiles.active`.

**Example (application.properties):**
```properties
spring.profiles.active=dev
```

**Example (application.yml):**
```yaml
spring:
  profiles:
    active: dev
```

## Using `@Profile` Annotation

The `@Profile` annotation is used to load beans or configurations specific to a profile:

```java
@Profile("dev")
@Bean
public DataSource devDataSource() {
    return new H2DataSource();
}

@Profile("prod")
@Bean
public DataSource prodDataSource() {
    return new PostgresDataSource();
}
```

**Explanation:** If `spring.profiles.active=dev`, the `devDataSource` bean (using H2 in-memory database) will be loaded. For `prod`, the `prodDataSource` bean (using PostgreSQL) will be loaded. This eliminates the need to maintain multiple configuration files manually.

## Use Cases for Profiling

| Scenario | Configuration | Benefit |
| --- | --- | --- |
| **Development** | H2 in-memory DB, debug logging, mock services | Fast iteration and testing |
| **Testing** | Test database, isolated services, test data | Reproducible and isolated tests |
| **Production** | Production DB, minimal logging, real services | Security, performance, and stability |

# Actuator
Monitoring and managing applications in production is essential to ensure stability and performance. Spring Boot Actuator provides built-in features to track application health, metrics, and internal state through easy-to-use endpoints.

- Exposes production-ready endpoints (like /actuator/health) to check application status
- Supports monitoring via HTTP endpoints and JMX integration
- Helps track metrics, performance, and system behavior for better management

![Spring Boot Starter Actuator](https://media.geeksforgeeks.org/wp-content/uploads/20250318160722633679/Spring-Boot-Starter-Actuator_.webp)

## Advantages of Actuator Application
- It increases customer satisfaction.
- It reduces downtime.
- It boosts productivity.
- It improves Cybersecurity Management.
- It increases the conversion rate.

## Setup and Configuration
### 1. Add Dependency
For Maven (pom.xml):
``` xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
</dependencies>
```
For Gradle (build.gradle):
``` gradle
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-actuator'
}
```

### **2 Exposing Endpoints**

By default, only the `/health` endpoint is visible for security reasons. You can manage visibility in your `application.properties`:

***Enable ** :`management.endpoint.metrics.enabled=true`  
An endpoint must be "enabled" to exist at all. Most are enabled by default, but you can turn specific ones off for performance or security.
* **Expose specific ones**: `management.endpoints.web.exposure.include=*`
Even if an endpoint is "enabled", it won't be visible over the web (HTTP) unless you "expose" it. By default, ONLY /health is exposed.
* **Expose specific ones**: `management.endpoints.web.exposure.include=health,info,metrics`  

* **Exclude endpoints**: `management.endpoints.web.exposure.exclude=env`
* **Change base path**: 
`management.endpoints.web.base-path=/monitoring` (changes `/actuator` to `/monitoring`)  
By default, all monitoring happens at http://localhost:8080/actuator. If you want to rename this (perhaps to hide it from bots or fit your company naming standards), you change the base-path.

---

### **3. Commonly Used Endpoints**

Actuator provides over 20 built-in endpoints. Here are the most useful:

| Endpoint | Description |
| --- | --- |
| **`/health`** | Shows basic application health status (UP/DOWN). |
| **`/metrics`** | Displays metrics like memory usage, garbage collection, and request counts. |
| **`/beans`** | Lists every Spring Bean registered in the Application Context. |
| **`/mappings`** | Shows all `@RequestMapping` paths and which controllers handle them. |
| **`/loggers`** | Allows you to view and even **change** logging levels at runtime. |
| **`/threaddump`** | Performs a thread dump to diagnose "stuck" or slow processes. |
| **`/caches`** | Exposes and allows management of available caches. |
| **`/conditions`** | Shows conditions evaluated on configuration and auto-configuration classes. |
| **`/httptrace`** | Displays HTTP trace information, typically for the last 100 requests. |
| **`/sessions`** | Allows retrieval and deletion of user sessions (requires Spring Session). |


### **4.Testing & Accessing Actuator APIs**
The primary entry point is the `/actuator` URL.

* **Default Access**: Visit `http://localhost:8080/actuator`.
* **Custom Path**: If you changed the base path in `application.properties` (e.g., `management.endpoints.web.base-path=/details`), use `http://localhost:8080/details`.
* **Function**: This provides a JSON response containing links to all other enabled and exposed endpoints.

---

The `health` ID is one of the few endpoints activated and exposed by default because it is essential for monitoring.

* **How to Access**: Navigate directly to `http://localhost:8080/actuator/health`.
* **Interpreting the Result**:
    * **Status: "UP"**: This indicates the application is healthy and all checked components (like the database) are functioning correctly.
    * **Status: "DOWN"**: This indicates a failure in one or more critical components.

# DevTools
Spring Boot DevTools is a module provided by Spring Boot to enhance the developer experience during application development. It helps improve productivity by reducing manual effort and speeding up the development cycle.

- Automatic Restart: Restarts the application automatically when code changes are detected
- Live Reload: Refreshes the browser automatically after changes
- Property Defaults: Applies sensible development-time configurations automatically
- Global Settings: Allows configuration across multiple projects
- Remote Debug Tunneling: Enables debugging of applications running in remote environments
![DevTools](https://media.geeksforgeeks.org/wp-content/uploads/20220219002901/devtools.jpg)



## Configuration & Installation

#### **Add Dependency**

For **Maven** (`pom.xml`):

```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-devtools</artifactId>
   <scope>runtime</scope>
</dependency>

```

For **Gradle** (`build.gradle`):

```gradle
dependencies {
    developmentOnly("org.springframework.boot:spring-boot-devtools")
}

```

#### **Common `application.properties` Settings**

* **Toggle DevTools**: `spring.devtools.restart.enabled=true/false`.
* **Exclude Resources**: `spring.devtools.restart.exclude=resources/,static/` (Prevents restart for these files).
* **Toggle LiveReload**: `spring.devtools.livereload.enabled=true/false`.

---

### How Automatic Restart Works

Unlike a full cold start, DevTools uses a **two-class loader** system to make restarts nearly instant:

* **Base Classloader**: Contains dependencies/libraries (like Spring JARs) that rarely change.
* **Restart Classloader**: Contains your application code (the files you are actively editing).
* **The Workflow**: When you change a Java file, only the **Restart Classloader** is reloaded. The JVM and base libraries stay loaded, which drastically reduces restart time.

> **Note**: Changes to project dependencies (e.g., adding a new library to `pom.xml`) require a **manual** restart because the Base Classloader is not automatically reloaded.

###  Productivity Tools

#### **Template Cache Disabling**
Normally, engines like **Thymeleaf**, **FreeMarker**, and **Groovy** cache templates to boost speed. In development, this is a nuisance because you can't see UI changes without a restart.

- Template caching is automatically disabled during development
- Changes in templates are reflected immediately after browser refresh
- Eliminates the need to restart the application for UI updates

#### **LiveReload Server**

DevTools includes an embedded **LiveReload server**.

* **Browser Sync**: If you use a LiveReload browser plugin (available for Chrome, Firefox, and Safari, not for Internet Explorer/Edge)), the browser will **automatically refresh** as soon as DevTools detects a change in your CSS, JS, or templates.


#### **H2 Database Console**

If an H2 database dependency is present, DevTools enables a web console.

* **URL**: `http://localhost:8080/h2-console`.
* **Purpose**: View and manage in-memory data handled by your application during development.

## DevTools Cheat Sheet

| Feature | Key Setting / URL | Impact on Development |
| --- | --- | --- |
| **Auto-Restart** | `spring.devtools.restart.enabled=true` | Reloads only your code (Restart Classloader) on save. |
| **Ignore Files** | `spring.devtools.restart.exclude=static/**` | Prevents server restarts for simple static asset changes. |
| **LiveReload** | `spring.devtools.livereload.enabled=true` | Triggers automatic browser refresh via embedded server. |
| **Template Caching** | `spring.thymeleaf.cache=false` (auto) | UI changes show up immediately without a restart. |
| **H2 Console** | `http://localhost:8080/h2-console` | Quick web-access to your in-memory database. |

# Introduction to RESTful Web Services
RESTful Web Services provide a standard way to build scalable and stateless web APIs using HTTP. In modern applications, REST APIs allow different systems such as web apps, mobile apps, and microservices to communicate efficiently.

- Spring Boot simplifies the creation of REST APIs using annotations and minimal configuration.
- REST services exchange data in formats such as JSON and XML, with JSON being the most widely used format.

## What is REST?
REST (Representational State Transfer) is an architectural style used for designing network-based applications. It allows different systems to communicate over HTTP using standard methods such as GET, POST, PUT, and DELETE.

- Introduced by Roy Thomas Fielding to simplify web communication using HTTP protocols.
- Widely used for building scalable and stateless web APIs in frameworks like Spring Boot.
![REST](https://media.geeksforgeeks.org/wp-content/uploads/20260309111549502778/Rest.webp)

## Key Concepts of RESTful Web Services

### 1. Resource
A resource is any object, data, or service that can be accessed by a client using a URI (Uniform Resource Identifier).

**Example:**
```
/users
/products
/orders
```

### 2. Stateless Communication
REST APIs are stateless, meaning every request from the client must contain all necessary information. The server does not store client session data between requests.

### 3. Representations
Resources can be represented in multiple formats when returned to the client. Common formats include:
- JSON
- XML
- HTML
- PDF

### 4. HTTP Verbs
REST APIs use standard HTTP methods to perform CRUD operations on resources.

## HTTP Methods in REST APIs

| HTTP Method | Operation | Description |
| --- | --- | --- |
| GET | Read | Retrieves existing data |
| POST | Create | Creates a new resource |
| PUT | Update | Updates an existing resource |
| DELETE | Delete | Removes a resource |

## HTTP Status Codes
REST APIs rely on these codes to communicate the result of client requests.

| Status Code | Meaning |
| --- | --- |
| 200 | Request successful |
| 201 | Resource created |
| 401 | Unauthorized access |
| 404 | Resource not found |
| 500 | Internal server error |

## Principles of RESTful Web Services
- **Resource Identification via URI:** Every resource has a unique URI.
- **Uniform Interface:** CRUD operations use standard HTTP methods: GET, POST, PUT, DELETE.
- **Self-Descriptive Messages:** The request and response contain all necessary information.
- **Stateless Interactions:** Each request is independent; no session data is stored on the server.
- **Cacheable:** Responses can be cached when appropriate to improve performance.

## Security Best Practices for REST APIs
- **Authentication and Authorization:** Use JWT or OAuth 2.0.
- **Input Validation:** Sanitize requests to prevent SQL injection and XSS attacks.
- **HTTPS Enforcement:** Ensure all communications are encrypted.
- **Rate Limiting:** Protect against abuse by limiting request rates.

## Advantages of RESTful Web Services
- **Simple and Lightweight:** Easier to develop and consume compared to SOAP(Simple Object Access Protocol)).
- **Client-Server Decoupling:** Enables independent development of client and server.
- **Scalable:** Stateless communication supports horizontal scaling.
- **Layered System Architecture:** Applications can be divided into layers, enhancing modularity and maintainability.
- **Cacheable:** Responses can be cached to improve performance and reduce bandwidth.

# REST Controller
A REST Controller in Spring Boot is a class annotated with `@RestController` that processes incoming HTTP requests and returns data objects (usually JSON) rather than views. It combines the functionality of `@Controller` and `@ResponseBody`.

### @ResponseBody
This annotation can be used at both the class and method levels.

It tells Spring that the return value does not need to be resolved to a view page like HTML or JSP. Instead, it is written directly to the HTTP response body.

The conversion from a Java object to JSON is handled by the Jackson project, which performs data binding under the hood.

### @RestController

The `@RestController` annotation marks a class as a RESTful controller where every method returns data instead of a view. Returned Java objects are automatically converted to JSON or XML by message converters.

Example:

```java
@RestController
public class HelloController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, Welcome to REST API!";
    }
}
```

### Explanation

- `@RestController` tells Spring this class handles REST API requests.
- `@GetMapping("/hello")` maps HTTP GET requests to the method.
- The method returns a String that Spring sends directly to the client.

### @Controller vs @RestController

| Feature | @Controller | @RestController |
|---|---|---|
| Purpose | Handles web requests and returns views | Sends data directly in response |
| Return Type | View name (HTML/JSP) | Raw data (JSON/XML/String) |
| View Resolver | Used | Not used |
| Usage | Web MVC applications | REST APIs |

## @RequestMapping

`@RequestMapping` is a flexible Spring annotation used at the class and method level to map web requests to specific controllers or handler methods. It helps define URL endpoints for handling HTTP requests in Spring Boot applications.

- Supports building REST APIs
- Allows multiple endpoints for a single resource
- Enables defining multiple endpoints in one `@RequestMapping` annotation

```java
@RequestMapping(value = "/path", method = RequestMethod.GET)
```

Parameters:

- `value` or `path` — Defines the URL path.
- `method` — Specifies the HTTP request method.

Instead of `method`, you can use these common request mapping annotations:

- `@GetMapping` — Retrieves data from the server without modifying it.
- `@PostMapping` — Creates or adds new data to the database (for example, a new student record).
- `@PutMapping` — Updates existing data in the database.
- `@DeleteMapping` — Removes existing data from the database.

## Implementation
### Create the Model Class

Create `Details.java` under `src/main/java`:

```java
public class Details {
    private int id;
    private String name;

    // Constructor
    public Details(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // Getters and Setters
    public int getId() { return id; }
    public void setId(int id) { this.id = id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```

### Create a REST Controller

Create `Controller.java`:

```java
import org.springframework.web.bind.annotation.*;
import java.util.*;

@RestController
@RequestMapping("/api")
public class Controller {
    private List<Details> detailsList = new ArrayList<>();

    // GET API → Fetch all details
    @GetMapping("/details")
    public List<Details> getAllDetails() {
        return detailsList;
    }

    // POST API → Add new detail
    @PostMapping("/details")
    public String addDetails(@RequestBody Details details) {
        detailsList.add(details);
        return "Data Inserted Successfully";
    }

    // PUT API → Update detail by ID
    @PutMapping("/details/{id}")
    public String updateDetails(@PathVariable int id, @RequestBody Details updatedDetails) {
        for (Details details : detailsList) {
            if (details.getId() == id) {
                details.setName(updatedDetails.getName());
                return "Data Updated Successfully";
            }
        }
        return "Detail not found!";
    }

    // DELETE API → Remove detail by ID
    @DeleteMapping("/details/{id}")
    public String deleteDetails(@PathVariable int id) {
        detailsList.removeIf(details -> details.getId() == id);
        return "Data Deleted Successfully";
    }
}
```

### Run the Application
1. Add a New Detail (POST Request)
Endpoint: POST http://localhost:8080/api/details
Request body:

```json
{
  "id": 1,
  "name": "John Doe"
}
```

Response: "Data Inserted Successfully"

2) Fetch All Details (GET)

Endpoint: GET http://localhost:8080/api/details

Response example:

```json
[
  {
    "id": 1,
    "name": "John Doe"
  }
]
```

3) Delete a Detail (DELETE)

Endpoint: DELETE http://localhost:8080/api/details/1

Response: "Data Deleted Successfully"

## `@PostMapping`

`@PostMapping` in Spring MVC is used to handle HTTP **POST** requests in RESTful web services. It maps a specific URL to a handler method that processes data sent from the client, typically through the request body.

- Used to create or submit data to the server.
- Data is usually received in the request body (e.g., JSON or form data).

### Example 1

```java
import org.springframework.web.bind.annotation.*;

@RestController
public class StudentController {

    @PostMapping("/addStudent")
    public String addStudent(@RequestBody String name) {
        return "Student " + name + " added successfully!";
    }
}
```

**Explanation:** The `addStudent` method is annotated with `@PostMapping`. It handles HTTP POST requests sent to the `/addStudent` URL. The student name is passed in the request body and processed by the method.

### Example 2

```java
import org.springframework.web.bind.annotation.*;

@RestController
public class StudentController {

    @PostMapping("/students/{id}")
    public String updateStudent(@PathVariable int id, @RequestBody Student student) {
        return "Student with ID " + id + " updated successfully!";
    }
}
```

**Explanation:** The `updateStudent` method is annotated with `@PostMapping`. It handles POST requests sent to the `/students/{id}` URL. The student ID is received as a path variable, and the updated student object is passed in the request body.

## `@GetMapping` Annotation

`@GetMapping` in Spring is used to handle HTTP **GET** requests in RESTful web services. It maps a specific URL to a controller method that retrieves data from the server.

- Used to retrieve or read data from the server.
- Parameters are usually passed through URL path variables or query parameters.

### Example 1

```java
@GetMapping("/students")
public List<Student> getAllStudents() {
    return studentRepository.findAll();
}
```

**Explanation:** `getAllStudents` is annotated with `@GetMapping`, so it is called when an HTTP GET request is received at `/students`.

### Example 2

```java
@RestController
public class StudentController {

    @GetMapping("/students/{rollNo}")
    public String getStudent(@PathVariable int rollNo) {
        return "Details of student with Roll No: " + rollNo;
    }
}
```

**Explanation:** The `getStudent` method is annotated with `@GetMapping`. It handles HTTP GET requests sent to `/students/{rollNo}`. The roll number is passed as a path variable to fetch student details.

## `@PostMapping` vs `@GetMapping`

| Feature | `@GetMapping` | `@PostMapping` |
|---|---|---|
| HTTP Method | Handles GET requests | Handles POST requests |
| Purpose | Used to retrieve data from the server | Used to send data to the server (create/update) |
| Data Location | Data is passed through URL parameters/query strings | Data is sent in the request body |
| Effect on Server | Does not modify server data | May modify or create server data |
| Common Use Case | Fetching records, loading pages, reading APIs | Form submissions, creating resources in APIs |

## `@DeleteMapping`

`@DeleteMapping` in Spring is used to handle HTTP DELETE requests in RESTful web services. It maps a specific URL to a controller method that deletes a resource from the server. It is a shortcut for `@RequestMapping(method = RequestMethod.DELETE)`.

- Used to delete a resource from the server
- Commonly used in REST APIs for removing records

### Example

```java
@RestController
public class StudentController {

    @DeleteMapping("/students/{id}")
    public String deleteStudent(@PathVariable int id) {
        return "Student with ID " + id + " deleted successfully!";
    }
}
```

**Explanation:** The `deleteStudent` method is annotated with `@DeleteMapping`. It handles DELETE requests sent to `/students/{id}`. The student ID is passed as a path variable to delete the specific student.

## `@PutMapping`

`@PutMapping` is used to handle HTTP PUT requests in a REST API. It maps a request to a controller method that updates an existing resource on the server. This annotation is commonly used when a client sends updated data to modify existing records.

- Used to handle HTTP PUT requests in Spring controllers
- Commonly used for updating existing resources in REST APIs

### Example

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @PutMapping("/{id}")
    public String updateUserName(@PathVariable int id, @RequestBody String name) {
        return "User with ID " + id + " updated with name " + name;
    }
}
```

**Explanation:** `@PutMapping("/{id}")` handles the HTTP PUT request to update a user's name. The `@PathVariable` annotation is used to get the user ID from the URL, while `@RequestBody` receives the new name sent in the request body. The method then processes the data and returns a confirmation message.

## `@DeleteMapping` vs `@PutMapping`

| Feature | `@PutMapping` | `@DeleteMapping` |
|---|---|---|
| HTTP Method | Handles HTTP PUT requests | Handles HTTP DELETE requests |
| Purpose | Used to update an existing resource | Used to delete an existing resource |
| Data Handling | Usually receives updated data in the request body | Usually requires only the resource ID to delete it |
| Data Location | Request body | URL path or query parameter |
| Effect on Server | Updates existing data | Removes existing data |
| Common Use Case | Updating user details, product price, etc. | Deleting a user, product, or record |

## `@PathVariable`

`@PathVariable` is used to extract values from the URI path of a request. It is commonly used in REST APIs where resources are identified directly within the URL.

- Binds a method parameter to a URI template variable
- Mostly used for identifying specific resources in RESTful endpoints

### Example:

```java
@GetMapping("/users/{id}")
public String getUserById(@PathVariable int id) {
    return "User ID: " + id;
}
```

**Explanation:** A GET API endpoint that retrieves the `id` value from the URL path using `@PathVariable` and returns it as part of the response.

## `@RequestParam`

`@RequestParam` is used to extract values from query parameters in the URL. It is commonly used when sending optional data, filters, or search parameters in requests.

- Binds a method parameter to a query parameter in the URL
- Can be required or optional, and also supports default values

### Example:

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/search")
    public String searchUser(@RequestParam String name) {
        return "Searching user with name: " + name;
    }
}
```

**Explanation:** `@RequestParam` extracts the `name` value from the query parameter in the URL. If the request is `/users/search?name=John`, the method receives `"John"` as the value of the name parameter.

## `@PathVariable` Vs `@RequestParam` Annotations

| Feature | `@PathVariable` | `@RequestParam` |
|---|---|---|
| **Definition** | Used to extract values from the URL path | Used to extract values from query parameters in the URL |
| **URL Position** | Value appears inside the URL path | Value appears after `?` as key-value pairs |
| **Purpose** | Mainly used to identify a specific resource like an ID | Mainly used to pass filters, search values, or optional data |
| **URL Example** | `/users/101` | `/users/search?name=John` |
| **Annotation Example** | `@GetMapping("/users/{id}")` | `@GetMapping("/users/search")` |

## `@RequestBody`

`@RequestBody` is an annotation in Spring MVC used to bind the HTTP request body to a method parameter in a controller. It automatically converts incoming JSON data into a Java object.

- Maps JSON data from the request body to a Java object.
- Commonly used in POST and PUT requests to receive client data.

### Syntax

```java
@PostMapping("/users")
public String createUser(@RequestBody User user) {
    return "User received: " + user.getName();
}
```

`@RequestBody` is used to get the request body from the incoming request.

## ResponseEntity

In Spring Boot, `ResponseEntity<T>` is a powerful wrapper that represents the entire **HTTP response**. It allows you to control the **Status Code**, **HTTP Headers**, and the **Response Body** programmatically.

---

### 1. Why Use `ResponseEntity`?

* **Full Control**: You can return different status codes based on logic (e.g., `201 Created` for success or `404 Not Found` if a resource is missing).
* **Header Customization**: Easily add custom headers for metadata or security.
* **Type Safety**: Use Generics (e.g., `ResponseEntity<User>`) to ensure the response body matches your model.

---

### 2. Common Implementation Patterns

#### A. Using Static Helper Methods (Quickest)

Spring provides shorthand methods for common status codes.

```java
// Return 200 OK with data
return ResponseEntity.ok(detailsList);

// Return 201 Created with data
return ResponseEntity.status(HttpStatus.CREATED).body("Resource Created");

// Return 404 Not Found
return ResponseEntity.notFound().build();

```

#### B. Using the Builder Pattern (Most Flexible)

Use the builder if you need to add custom headers or complex configurations.

```java
@GetMapping("/details/{id}")
public ResponseEntity<Details> getDetail(@PathVariable int id) {
    Details data = findDetailById(id);
    
    return ResponseEntity.ok()
        .header("Custom-Header", "Value")
        .header("Cache-Control", "no-cache")
        .body(data);
}

```

---

### 3. Comparison: `@ResponseBody` vs. `ResponseEntity`

| Feature | `@ResponseBody` | `ResponseEntity<T>` |
| --- | --- | --- |
| **Status Code** | Always `200 OK` (unless exception thrown) | **Fully Dynamic** (200, 201, 400, 404, etc.) |
| **Headers** | Limited to default headers | **Fully Customizable** |
| **Flexibility** | Simple, but rigid | High; best for professional APIs |
| **Usage** | Added to methods or via `@RestController` | Returned as the method result |

---

### 4. Practical Example (CRUD Application)

Integrating `ResponseEntity` with the `POST`, `PUT`, and `DELETE` methods you previously drafted:

```java
// POST: Return 201 Created instead of just a String
@PostMapping("/details")
public ResponseEntity<String> addDetails(@RequestBody Details details) {
    detailsList.add(details);
    return new ResponseEntity<>("Data Inserted", HttpStatus.CREATED);
}

// DELETE: Return 204 No Content if successful
@DeleteMapping("/details/{id}")
public ResponseEntity<Void> deleteDetails(@PathVariable int id) {
    boolean removed = detailsList.removeIf(d -> d.getId() == id);
    return removed ? ResponseEntity.noContent().build() : ResponseEntity.notFound().build();
}

```

---

### 💡 Summary Table for your Cheat Sheet

| HTTP Status | ResponseEntity Method | Typical Use Case |
| --- | --- | --- |
| **200 OK** | `.ok(body)` | Successful `GET` or `PUT`. |
| **201 Created** | `.status(HttpStatus.CREATED).body(b)` | Successful `POST` (new resource created). |
| **204 No Content** | `.noContent().build()` | Successful `DELETE` (no body needed). |
| **400 Bad Request** | `.badRequest().body(error)` | Invalid input from the client. |
| **404 Not Found** | `.notFound().build()` | Resource with specific ID does not exist. |

---

## JSON (JavaScript Object Notation)

JSON is the most commonly used format for exchanging data between clients and servers in REST APIs. Spring Boot simplifies working with JSON by automatically converting Java objects to JSON (serialization) and JSON to Java objects (deserialization) using the Jackson library.

### Key Concepts

- **Serialization**: Converting Java objects into JSON to send to clients.
- **Deserialization**: Converting JSON from clients into Java objects.

When you use `@RequestBody`, Spring Boot automatically deserializes the incoming JSON payload into a Java object. Similarly, when you return a Java object from a controller method, Spring Boot automatically serializes it to JSON for the HTTP response.

## Jackson - JSON Processing
Jackson is a popular Java library for JSON processing. Spring Boot automatically configures Jackson via the `spring-boot-starter-web` dependency. This means you don't need to manually add Jackson unless you need additional modules (e.g., `jackson-datatype-jsr310` for date/time formatting).

- **Automatic Configuration**: No manual setup required with Spring Boot
- **JSON Serialization/Deserialization**: Converts Java objects to JSON and vice versa
- **Customizable**: Use annotations to control JSON output format
- **Module Support**: Additional modules available for specific data types

### Common Jackson Annotations

| Annotation | Description |
| --- | --- |
| `@JsonProperty` | Rename a field in JSON |
| `@JsonIgnore` | Ignore a field during serialization/deserialization |
| `@JsonInclude` | Include/exclude fields based on conditions |
| `@JsonFormat` | Define format for date/time fields |
| `@JsonIgnoreProperties` | Ignore multiple fields |

### Example Usage

```java
import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonFormat;
import java.time.LocalDate;

public class Student {
    
    @JsonProperty("student_id")
    private int id;
    
    @JsonProperty("full_name")
    private String name;
    
    @JsonIgnore
    private String internalNotes;
    
    @JsonFormat(pattern = "yyyy-MM-dd")
    private LocalDate dateOfBirth;
    
    // Getters and Setters
}
```
This cheat sheet covers the architecture and implementation of a professional exception handling system in Spring Boot, transforming raw errors into meaningful client responses.

# Spring Boot Exception Handling Architecture

Exception handling ensures your API is **robust** (doesn't crash) and **informative** (tells the client exactly what went wrong).

### 1. The Three Approaches

| Method | Scope | Best Use Case |
| --- | --- | --- |
| **Default Handling** | Global (Fall-back) | For unhandled/unexpected system errors. |
| **`@ExceptionHandler`** | Local (Controller) | For errors specific to one resource (e.g., `Customer`). |
| **`@ControllerAdvice`** | Global (Centralized) | For common errors across the entire app (e.g., `404 Not Found`). |

---

## 🛠️ Step-by-Step Implementation

### Step 1: Create Custom Exceptions

Always extend `RuntimeException` so you don't force every method to use a `throws` clause.

```java
public class CustomerAlreadyExistsException extends RuntimeException {
    public CustomerAlreadyExistsException(String msg) {
        super(msg);
    }
}

```

### Step 2: Create a Standard Error Response

Define a consistent JSON structure so your frontend knows exactly what to expect when an error occurs.

```java
@Data @AllArgsConstructor
public class ErrorResponse {
    private int statusCode;
    private String message;
}

```

### Step 3: Global Handling with `@ControllerAdvice`

This class acts as an interceptor. If any controller throws `NoSuchCustomerExistsException`, this method catches it and returns a `404`.

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(NoSuchCustomerExistsException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public @ResponseBody ErrorResponse handleNoSuchCustomer(NoSuchCustomerExistsException ex) {
        return new ErrorResponse(HttpStatus.NOT_FOUND.value(), ex.getMessage());
    }
}

```

---

## 🔄 Service Layer Logic

Throw your custom exceptions in the Service Layer when business rules are broken.

```java
public String addCustomer(Customer customer) {
    if (repository.existsById(customer.getId())) {
        // This triggers the ExceptionHandler
        throw new CustomerAlreadyExistsException("Customer already exists!!");
    }
    repository.save(customer);
    return "Added successfully";
}

```

---

## 💡 Summary Cheat Sheet

| Annotation | Description |
| --- | --- |
| **`@ExceptionHandler`** | Marks a method to handle a specific exception. Returns a custom body. |
| **`@ResponseStatus`** | Defines the HTTP Status code (e.g., `CONFLICT`, `NOT_FOUND`) for the response. |
| **`@ControllerAdvice`** | Intercepts exceptions from **all** controllers. Centralizes your "error logic." |
| **`@ResponseBody`** | Ensures the `ErrorResponse` object is converted to JSON for the client. |

### Why use Global Handling?

1. **DRY (Don't Repeat Yourself):** Write the "NotFound" logic once; use it for Customers, Tickets, and Orders.
2. **Clean Controllers:** Your controllers focus on successful paths; the `GlobalExceptionHandler` focuses on the failures.
3. **Professionalism:** Clients receive a clean JSON like `{"statusCode": 409, "message": "User exists"}` instead of a 500-line StackTrace.
---

### 1. Why does Spring prefer Unchecked Exceptions?

In Java, **checked exceptions** (like `SQLException`) force the developer to either catch the error or declare it in the method signature (`throws`). Spring intentionally converts these into **unchecked exceptions** (subclasses of `RuntimeException`) for several reasons:

* **Reduces Boilerplate**: You no longer need `try-catch` blocks everywhere for errors you can't actually fix at that level (like a database being down).
* **Decouples Code**: If your Service layer throws a `SQLException`, it is now "leaking" implementation details. If you switch to a different data source, you’d have to change your method signatures. Unchecked exceptions remove this dependency.
* **Encourages Clean Architecture**: It allows business logic to remain focused on the "happy path," while error handling is moved to a centralized location (like a `@ControllerAdvice`).
* **Flexibility**: Developers can still catch the exceptions if they want to, but they aren't *forced* to by the compiler.

---

### 2. The Spring Data Access Exception Hierarchy

```
java.lang.Object
  └── java.lang.Throwable
      ├── java.lang.Error
      │   ├── OutOfMemoryError
      │   ├── StackOverflowError
      │   └── VirtualMachineError
      └── java.lang.Exception
          ├── IOException (Checked)
          ├── SQLException (Checked)
          ├── ClassNotFoundException (Checked)
          └── RuntimeException (Unchecked)
              ├── NullPointerException
              ├── IllegalArgumentException
              ├── IndexOutOfBoundsException
              └── NumberFormatException
```
Spring provides a sophisticated hierarchy for data-related errors. When using Spring Data or JDBC Template, Spring catches low-level, vendor-specific exceptions (like MySQL or Oracle error codes) and **translates** them into its own consistent hierarchy.

#### Key Characteristics:

* **Root Class**: All exceptions extend `DataAccessException`, which is an **unchecked** exception.
* **Portable**: Whether you use Hibernate, JPA, or JDBC, you receive the same Spring exceptions.
* **Descriptive**: Instead of a generic `SQLException`, Spring gives you a specific subclass that tells you exactly what went wrong.

#### Common Subclasses:

| Exception | Meaning |
| --- | --- |
| **`DataIntegrityViolationException`** | Thrown when a constraint is violated (e.g., trying to insert a duplicate primary key). |
| **`EmptyResultDataAccessException`** | Thrown when a result was expected (like `findOne`), but the database returned nothing. |
| **`DataAccessResourceFailureException`** | The connection to the database/resource failed. |
| **`OptimisticLockingFailureException`** | Occurs when two users try to update the same record simultaneously and a conflict occurs. |
| **`TypeMismatchDataAccessException`** | Thrown if the data in the DB cannot be mapped to the Java field type. |

| Feature | Standard Java (JDBC) | Spring Data Access |
| --- | --- | --- |
| Main Exception | java.sql.SQLException | org.springframework.dao.DataAccessException |
| Exception Type | Checked (Forces try-catch) | Unchecked (Cleaner code) |
| Specificity | Generic (One error for everything) | Specific (Separate error for "Constraint", "Connection", etc.) |
| Vendor Neutral | No (Error codes differ by DB) | Yes (Same exception for MySQL, H2, or Oracle) |

---
> **Peer Note:** This is why we usually don't catch exceptions in the Repository or Service layers. We let them bubble up to the `GlobalExceptionHandler`, where we can turn a `DataIntegrityViolationException` into a clean **409 Conflict** response for the user.