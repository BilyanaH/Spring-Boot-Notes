# Spring Boot Cheat Sheet

_[geeksforgeeks.org - resourse for this markdown file](https://www.geeksforgeeks.org/advance-java/spring-boot/)_

_[medium.com - interview questions](https://medium.com/@lakshyachampion/spring-boot-essentials-the-interview-cheat-sheet-e81ee59ce646)_
## Table of Contents

### Fundamentals
- [Spring](#spring)
- [Spring Boot](#spring-boot)
- [Spring MVC](#spring-mvc)

### Architecture & Configuration
- [Spring Boot Architecture](#spring-boot-architecture)
  - [Architecture Layers](#spring-boot-architecture-layers)
  - [Flow Architecture](#spring-boot-flow-architecture)

### Core Concepts
- [Annotations](#annotations)
- [Spring Injection](#spring-injection)
- [BeanFactory vs ApplicationContext](#beanfactory-vs-applicationcontext-in-spring)

### Dependency Injection
- [Spring Autowiring](#spring-autowiring)
- [`@Autowired` and `@Qualifier`](#autowired-and-qualifier)

### Bean Management
- [Bean Life Cycle](#bean-life-cycle)
- [Singleton and Prototype Scopes](#singleton-and-prototype-bean-scopes)
- [Custom Bean Scope](#custom-bean-scope)
- [3 Ways to Create Spring Beans](#3-ways-to-create-spring-beans)

### Advanced Topics
- [Dispatcher Servlet in Spring](#what-is-dispatcher-servlet-in-spring)
- [Introduction to Build Tools](#introduction-to-build-tools)
- [Spring Boot Auto-Configuration](#spring-boot-auto-configuration)
 
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

Used in the DAO layer to interact with the database. Automatically translates database-related exceptions into Spring exceptions.

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

## Validation Annotations

Validation annotations ensure input data correctness.

- `@NotNull` - Field value must not be null
- `@NotBlank` - String must contain at least one non-whitespace character
- `@Email` - Validates email format
- `@Size` - Restricts field length or size

Example:

```java
public class User {
    @NotBlank
    private String username;

    @Email
    private String email;
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

# What is Dispatcher Servlet in Spring?
The **Dispatcher Servlet** is the "Front Controller" of a Spring Web application. It acts as the single entry point for every HTTP request coming into your app.

DispatcherServlet in Spring is the central component of the Spring MVC framework that acts as the front controller. It receives all incoming HTTP requests, forwards them to the appropriate controllers, and manages the response generation process including handler mapping and view resolution.

- It handles incoming requests and routes them to the appropriate controllers
- It tells controllers how to handle requests and return responses.
- After the controllers process the request, it picks the correct view to show the result (like a webpage).



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
## Singleton Scope
The Singleton scope is the default scope in Spring. In this scope, the Spring container creates only one instance of the bean and shares it across the entire application.

- The same object is shared across all components.
- Created when the application context starts (by default).
- Suitable for stateless services such as service classes and repositories 

## Prototype Scope
In the Prototype scope, the Spring container creates a new bean instance every time it is requested from the container. Unlike singleton, each request gets a completely new object.

- Multiple objects are created.
- A new instance is returned every time getBean() is called.
- The container manages creation only, not the full lifecycle.

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

## Gradle
- Philosophy: Flexibility and Performance. Uses a Domain Specific Language (DSL).
- Config: Uses build.gradle (Groovy or Kotlin).
- Pros: Highly customizable, faster (incremental builds), standard for Android.
- Cons: Steeper learning curve.


# Spring Boot Auto-Configuration
Spring Boot Auto-Configuration is a feature that automatically configures application components based on the dependencies available in the classpath.

- Creates and configures required beans, services, and settings automatically
- Reduces manual configuration and speeds up development

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