# Table of Contents

- [Spring Boot Core Basics](#spring-boot-core-basics)  
- [Annotations](#annotations)  
- [Starters and Dependencies](#starters-and-dependencies)  
- [Auto-Configuration](#auto-configuration)  
- [Embedded Servers and Configuration](#embedded-servers-and-configuration)  
- [Application Startup and Flow](#application-startup-and-flow)  
- [Spring Boot Actuator](#spring-boot-actuator)  
- [Profiles and Properties](#profiles-and-properties)  
- [Dependency Injection and IoC](#dependency-injection-and-ioc)  
- [Spring Data JPA and Database](#spring-data-jpa-and-database)  
- [Spring MVC and Thymeleaf](#spring-mvc-and-thymeleaf)  
- [Development Tools and CLI](#development-tools-and-cli)  
- [Web vs Non-Web Applications](#web-vs-non-web-applications)  
- [Beans and Application Context](#beans-and-application-context)  
- [Deployment](#deployment)

---
---

### Spring Boot Core Basics

## 🔹 What is Spring Boot?

**Spring Boot** is a framework built on top of the Spring framework to **create stand-alone, production-grade web applications** with minimal configuration.  
--standalone means that the application can run independently without requiring an external application server like Tomcat or Jetty to be installed separately.
Key points:

- No need for external servers — uses **embedded servers** like Tomcat or Jetty.
- Simplifies the creation of **RESTful applications**.
- Reduces boilerplate code and improves developer productivity.
- Creates **executable Spring applications** that are production-ready.

---

## 🔹 Features of Spring Boot

1. **Auto-configuration**  
   - Automatically configures dependencies using `@EnableAutoConfiguration`.  
   - Reduces boilerplate setup and manual configuration.

2. **Spring Boot Starter POM**  
   - Pre-configured dependencies for common functionalities (database, security, web, etc.).
   - Simplifies project setup and dependency management.

3. **Spring Boot CLI (Command Line Interface)**  
   - Command-line tool for creating, running, and managing Spring Boot projects.

4. **Actuator**  
   - Provides endpoints for **health checks, metrics, monitoring**, and troubleshooting.

5. **Embedded Servers**  
   - Supports embedded Tomcat, Jetty, and Undertow, enabling apps to run standalone without external servers.

---

## 🔹 Advantages of Spring Boot

| Advantage | Explanation |
|-----------|-------------|
| **Easy to use** | Reduces boilerplate code required for Spring applications. |
| **Rapid Development** | Auto-configuration and opinionated defaults enable faster app development. |
| **Scalable** | Applications can be scaled easily based on requirements. |
| **Production-ready** | Provides health checks, metrics, and externalized configuration for production use. |

---

## 🔹 Key Components of Spring Boot

1. **Spring Boot Starters** — Predefined dependencies for common tasks.  
2. **Auto-configuration** — Automatically sets up beans and configurations based on included dependencies.  
3. **Spring Boot Actuator** — Monitoring and management endpoints for applications.  
4. **Spring Boot CLI** — Tool for running and managing Spring Boot projects.  
5. **Embedded Servers** — Self-contained server support (Tomcat, Jetty) for running applications standalone.

---

## 🔹 Why Prefer Spring Boot over Spring?

| Feature | Spring | Spring Boot |
|---------|--------|-------------|
| **Ease of use** | More complex | Easier and faster setup |
| **Production readiness** | Less production-ready | Fully production-ready with monitoring |
| **Scalability** | Limited | Highly scalable |
| **Speed** | Slower | Rapid development with auto-configuration |
| **Customization** | Limited | Flexible and customizable |

---
# Spring Boot Architecture

Spring Boot simplifies Spring-based application development with a **layered architecture**:

---

## 1. **Spring Core**
- Manages **Dependency Injection (DI)** and **Inversion of Control (IoC)**.
- Handles **beans and application context**.

---

## 2. **Spring Boot Starters**
- Pre-configured **dependency templates** for common functionalities.
- Examples: `spring-boot-starter-web`, `spring-boot-starter-data-jpa`, `spring-boot-starter-security`.

---

## 3. **Auto-Configuration**
- Automatically configures beans based on **classpath dependencies**.
- Reduces manual setup via `@EnableAutoConfiguration`.

---

## 4. **Embedded Servers**
- Uses **Tomcat, Jetty, or Undertow**.
- Enables **standalone execution** without external servers.

---

## 5. **Spring Boot Actuator**
- Provides **monitoring and management endpoints**.
- Examples: `/actuator/health`, `/actuator/metrics`.

---

## 6. **Application Properties & Profiles**
- External configuration via `application.properties` or `application.yml`.
- Supports **multi-environment setups** with `@Profile`.

---



## 🔹 Internal Working of Spring Boot

1. **Create a new Spring Boot project** — using Spring Initializr or CLI.  
2. **Add dependencies** — web, data, security, etc., using starter POMs.  
3. **Annotate the application** — e.g., `@SpringBootApplication`, `@RestController`, `@Service`.  
4. **Run the application** — via embedded server (Tomcat/Jetty) as a standalone executable.  
5. **Auto-configuration and Bean creation** — Spring Boot automatically configures beans and resources based on dependencies.  
6. **Monitoring & Management** — Optional actuator endpoints provide application health, metrics, and environment info.

---

# Basic Spring Boot Annotations

- **@SpringBootApplication**  
  The main annotation used to bootstrap a Spring Boot application.  
  Combines:
  - `@Configuration`
  - `@EnableAutoConfiguration`
  - `@ComponentScan`  
  Typically placed on the main class of the application.

- **@Configuration**  
  Indicates that a class contains configuration methods for the application context.  
  Often used with `@Bean` annotations to define beans and their dependencies.

- **@Component**  
  Generic annotation for any Spring-managed component.  
  Marks a class as a Spring bean to be managed by the Spring container.

- **@RestController**  
  Defines a RESTful web service controller.  
  Specialized version of `@Controller` with `@ResponseBody` included by default.

- **@RequestMapping**  
  Maps HTTP requests to specific methods in a controller.  
  Can be applied:
  - At the class level for a base URL
  - At the method level for a specific URL mapping

---
---

### Annotations

# Spring Boot Core Annotations — Interview Notes

---

## 🔹 @SpringBootApplication

- **Purpose:** Main annotation to bootstrap a Spring Boot application.  
- **Internal Composition:**  
  `@SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan`
  
  1. **@Configuration** — Defines configuration class and beans.  
  2. **@EnableAutoConfiguration** — Automatically configures beans based on classpath dependencies.  
  3. **@ComponentScan** — Scans the package of the annotated class and its sub-packages for Spring components (@Component, @Service, etc.).  

- **Usage:** Typically placed on the main class with the `run()` method.

---

## 🔹 @RestController

- **Purpose:** Shortcut for creating RESTful services.  
- **Internal Composition:**  
  `@RestController = @Controller + @ResponseBody`  
  - **@Controller:** Marks the class as a request handler.  
  - **@ResponseBody:** Converts method return values directly into HTTP responses (JSON, XML).  

- **Usage:**  
  - Define endpoints for GET, POST, PUT, DELETE.  
  - Map request parameters to method arguments.  

---

## 🔹 Difference between @Controller and @RestController

| Feature | @Controller | @RestController |
|---------|------------|----------------|
| **Usage** | Marks a class as a controller | Combines @Controller + @ResponseBody |
| **Application** | Used for web applications | Used for RESTful APIs |
| **Request Handling** | With @RequestMapping, renders views | Handles GET, PUT, POST, DELETE and returns data directly |

> Note: Both handle requests, but `@RestController` is preferred for API development.

---

## 🔹 Difference between @RequestMapping and @GetMapping

| Feature | @RequestMapping | @GetMapping |
|---------|----------------|-------------|
| **Purpose** | Handles multiple HTTP methods (GET, POST, PUT, DELETE) | Specifically handles HTTP GET requests |
| **Example** | `@RequestMapping(value="/example", method=RequestMethod.GET)` | `@GetMapping("/example")` |

---

## 🔹 Difference between @SpringBootApplication and @EnableAutoConfiguration

| Feature | @SpringBootApplication | @EnableAutoConfiguration |
|---------|----------------------|-------------------------|
| **When to Use** | Default auto-configuration | Customize auto-configuration |
| **Entry Point** | Typically on main application class | Any configuration class, can work with @SpringBootApplication |
| **Component Scanning** | Includes @ComponentScan automatically | Does not scan components |
| **Example** | `@SpringBootApplication public class MyApp { public static void main(String[] args) { SpringApplication.run(MyApp.class, args); } }` | `@Configuration @EnableAutoConfiguration public class MyConfig { }` |

---

## 🔹 @ComponentScan

- **Purpose:** Tells Spring which packages to scan for components, services, and configurations.  
- **Usage Options:**  
  - Without arguments: Scans the package of the class.  
  - With `basePackages`: Scan specific packages.  
  - With `basePackageClasses`: Scan packages of specific classes.

---

## 🔹 Summary of @RequestMapping and @RestController

- **@RequestMapping:** Maps HTTP requests to handler methods. Can map by:
  - HTTP method (GET, POST, PUT, DELETE)  
  - URL path  
  - URL parameters  
  - Request headers

- **@RestController:** Marks a controller where every method returns data directly.  
  - Combines `@Controller + @ResponseBody`  
  - Simplifies creation of RESTful APIs.

---

### 📘 Core Spring Boot Annotations

#### 1. **@Controller**
- Used to mark a class as a **Spring MVC Controller**.
- Handles **web requests** and returns **views (HTML pages)**.
- Commonly used in traditional web applications (not REST APIs).

```java
@Controller
public class HomeController {
    @GetMapping("/home")
    public String home() {
        return "home"; // returns view name (home.html)
    }
}
```

---

#### 2. **@RestController**
- Combines `@Controller` and `@ResponseBody`.
- Used for **RESTful APIs** — directly returns data (like JSON/XML) instead of views.

---

#### 3. **@Service**
- Marks a class as a **service layer** component.
- Used to hold **business logic**.
- Makes the class eligible for **component scanning and dependency injection**.

```java
@Service
public class UserService {
    public String getUser() {
        return "Purvesh";
    }
}
```

---

#### 4. **@Repository**
- Used on **DAO (Data Access Object)** classes.
- Indicates that the class interacts with the **database**.
- Provides **automatic exception translation** (converts SQL exceptions into Spring DataAccessExceptions).

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> { }
```

---

#### 5. **@Component**
- The **generic stereotype** for any Spring-managed bean.
- Used when a class doesn’t fit into Controller, Service, or Repository layers.
- Spring automatically detects it using **component scanning**.

```java
@Component
public class EmailValidator {
    public boolean isValid(String email) { ... }
}
```

---

#### 6. **@Autowired**
- Used for **automatic dependency injection**.
- Spring automatically injects the required bean by **type**.

```java
@Autowired
private UserService userService;
```

---

#### 7. **@Qualifier**
- Used **with @Autowired** when multiple beans of the same type exist.
- Helps specify **which bean** should be injected.

```java
@Autowired
@Qualifier("emailService")
private NotificationService notificationService;
```

---

#### 8. **@GetMapping**
- Handles **HTTP GET requests**.
- Commonly used to **fetch data**.

```java
@GetMapping("/users")
public List<User> getUsers() { ... }
```

---

#### 9. **@PostMapping**
- Handles **HTTP POST requests**.
- Commonly used to **create new data**.

```java
@PostMapping("/users")
public User createUser(@RequestBody User user) { ... }
```

---
---

### Starters and Dependencies

## ⚙️ Spring Boot Starter Dependencies & Dependency Management

---

### 🧩 7. What are the Spring Boot Starter Dependencies?

Spring Boot provides **starter dependencies** — a set of convenient dependency bundles to simplify project setup.  
Each starter includes a curated list of libraries for specific functionalities, ensuring compatibility.

**Common Spring Boot Starters:**
- **spring-boot-starter-data-jpa** → For database access using Spring Data JPA.
- **spring-boot-starter-web** → For building RESTful web applications.
- **spring-boot-starter-security** → For securing applications.
- **spring-boot-starter-test** → For unit and integration testing.
- **spring-boot-starter-thymeleaf** → For building web applications with Thymeleaf templates.

---

### 📦 13. What is Spring Boot Dependency Management?

Spring Boot **dependency management** ensures all dependencies are:
- **Compatible** with the Spring Boot version used.
- **Automatically versioned**, avoiding conflicts.
- **Easy to add** — just include the starter, and all transitive dependencies are managed.

📘 Example:
If you want to create a web application, just include:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

📸 **Visual Overview:**
![Spring Boot Dependency Management](https://media.geeksforgeeks.org/wp-content/uploads/20231222123658/Spring-Boot-Interview-Questions--3.png)

---

### 🚀 15. What is the Starter Dependency of the Spring Boot Module?

**Spring Boot Starters** are pre-configured sets of dependencies designed for specific functionalities like web, data, or security.

They handle:
- **Required dependencies**
- **Version control**
- **Auto-configuration**

📘 Example: To add a web starter dependency

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

✅ **Key Benefits:**
- Reduces manual dependency management.
- Prevents version conflicts.
- Speeds up development.

---
---

### Auto-Configuration

## ⚙️ Auto-Configuration in Spring Boot

---

### 🔹 What is AutoConfiguration?

**Auto-Configuration** is one of Spring Boot’s key features that automatically configures your application based on the dependencies present in your project.  
It eliminates the need for manual setup by intelligently applying configuration defaults.

✅ **Example:**  
If `spring-boot-starter-web` is present, Spring Boot automatically:
- Configures **Tomcat** as the default web server.
- Sets up **DispatcherServlet**.
- Configures **Jackson** for JSON serialization.

📘 **Annotation Used:**  
`@EnableAutoConfiguration`  
This tells Spring Boot to start auto-configuring beans based on what it finds on the classpath.

---

### ❌ 18. How to Disable a Specific Auto-Configuration Class?

Sometimes you may want to **exclude** certain auto-configurations that are not required or that conflict with custom configurations.

You can disable specific classes using the **`exclude`** attribute of the `@EnableAutoConfiguration` annotation.

📘 **Syntax:**
```java
@EnableAutoConfiguration(exclude = { DataSourceAutoConfiguration.class })
```

📘 **Alternative (recommended way):**
You can also exclude using the `@SpringBootApplication` annotation:
```java
@SpringBootApplication(exclude = { SecurityAutoConfiguration.class })
```

✅ **Use case example:**  
If you don’t need Spring Security auto-configured, exclude it to prevent unnecessary security prompts.

---
---

### Embedded Servers and Configuration

## 🌐 Embedded Servers and Configuration in Spring Boot

---

### 🔹 14. Changing the Port of Embedded Tomcat Server

Yes, it’s possible to change the port of the **embedded Tomcat server** in Spring Boot.

By default, Spring Boot runs the application on **port 8080**.  
You can change it by adding this property in `application.properties`:

```properties
server.port=8081
```

✅ **Alternatively**, if you’re using `application.yml`:
```yaml
server:
  port: 8081
```

---

### 🔹 16. What is the Default Port of Tomcat in Spring Boot?

The **default port** of the embedded Tomcat server is **8080**.  
It can be changed using the `server.port` property as shown above.

---

### 🔹 17. Can We Disable the Default Web Server?

Yes ✅  
You can disable the **embedded web server** (Tomcat/Jetty/Undertow) by setting the port to **-1**.

📘 **Example:**
```properties
server.port=-1
```

This is useful when you are running **non-web** Spring Boot applications like CLI tools or batch jobs.

---

### 🔹 26. Difference Between WAR and Embedded Containers

| Feature | WAR | Embedded Containers |
|----------|-----|----------------------|
| **Packaging** | Contains all files needed to deploy to an external web server. | Includes the web server (Tomcat/Jetty) within the same JAR file. |
| **Configuration** | Requires external configuration files (like `web.xml`, `context.xml`). | Uses internal configuration properties and annotations. |
| **Deployment** | Deployed to external servers like Tomcat or JBoss. | Runs independently with `java -jar app.jar`. |
| **Security** | Can rely on web server-level security settings. | Can use built-in Spring Boot and JRE security features. |

---

✅ **In short:**
- **WAR** → Used for external deployment (traditional style).  
- **Embedded container (JAR)** → Used for standalone Spring Boot apps (modern approach).

---
---

### Application Startup and Flow

## ⚙️ Application Startup and Request Flow in Spring Boot

---

### 🔹 8. How Does a Spring Boot Application Get Started?

A **Spring Boot application** starts with the `main()` method, where the `@SpringBootApplication` annotation marks the entry point of the application.  
The `SpringApplication.run()` method bootstraps the application — it sets up the **Spring ApplicationContext**, **auto-configuration**, and starts the **embedded server** (like Tomcat).

📘 **Example:**
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

✅ **Key Steps:**
1. `@SpringBootApplication` triggers auto-configuration, component scanning, and bean initialization.
2. `SpringApplication.run()` creates and refreshes the **ApplicationContext**.
3. The **embedded server (Tomcat/Jetty)** starts automatically.
4. The application becomes ready to handle incoming HTTP requests.

---

### 🔹 20. Flow of HTTP Requests in a Spring Boot Application

The HTTP request flow in a Spring Boot application follows a layered architecture:

1. **Client Layer:**  
   The client (browser, Postman, etc.) sends an **HTTP request** (GET, POST, PUT, DELETE) to the application.

2. **Controller Layer:**  
   The **Controller** (annotated with `@RestController` or `@Controller`) receives the request and maps it to a handler method using annotations like `@RequestMapping` or `@GetMapping`.

3. **Service Layer:**  
   Contains the **business logic** of the application. It processes data and communicates with the repository layer.

4. **Repository Layer:**  
   Handles all **database operations** using **Spring Data JPA** (CRUD — Create, Read, Update, Delete).

5. **Response:**  
   The processed data or view (HTML/JSP/JSON) is sent back to the client as a response.

📊 **Request Flow Diagram:**  
![Spring Boot Request Flow](https://media.geeksforgeeks.org/wp-content/uploads/20241127172958716123/springboot---------interview---------questions.webp)

---

✅ **In short:**
> Client → Controller → Service → Repository → Database → Response to Client

---
---

### Spring Boot Actuator

## ⚙️ Spring Boot Actuator

---

### 🔹 27. What is Spring Boot Actuator?

**Spring Boot Actuator** is a module in Spring Boot that provides **production-ready features** such as monitoring, metrics, and health checks for your application.  
It helps developers and DevOps teams **track application health, performance, and behavior** in real-time — without writing extra code.

📘 **Key Features:**
- Provides **built-in endpoints** for monitoring (e.g., `/actuator/health`, `/actuator/info`, `/actuator/metrics`).
- Offers **integration with tools** like Prometheus, Grafana, and Spring Boot Admin.
- Supports **custom endpoints** for application-specific monitoring.

> 📝 **Note:** To use Actuator, simply add the dependency:  
> `spring-boot-starter-actuator`

---

### 🔹 28. How to Enable Actuator in a Spring Boot Application?

To enable and use Actuator in your Spring Boot project:

#### ✅ **Steps:**

1. **Add the Actuator dependency** to `pom.xml`:
   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-actuator</artifactId>
   </dependency>
   ```

2. **Enable endpoints** in `application.properties`:
   ```properties
   management.endpoints.web.exposure.include=*
   management.endpoint.health.show-details=always
   ```

3. **Run the Application.**
   Start your Spring Boot app, and access endpoints like:
   ```
   http://localhost:8080/actuator/health
   http://localhost:8080/actuator/info
   ```

---

✅ **In short:**
> **Spring Boot Actuator** = Real-time Monitoring + Health Check + Metrics + Management Endpoints

--- 
---

### Profiles and Properties

## 🌿 Spring Boot Profiles & Logging

---

### 🔹 25. What are Profiles in Spring?

**Spring Profiles** allow you to define **different configurations for different environments** — such as *development*, *testing*, and *production*.

📘 **Key Points:**
- Helps isolate environment-specific configurations (like database URLs or API keys).  
- Uses the `@Profile` annotation to specify which beans/configurations belong to which profile.
- You can **activate a profile** using:
  ```properties
  spring.profiles.active=dev
  ```
  or via command-line:
  ```bash
  java -jar app.jar --spring.profiles.active=prod
  ```

✅ **Example:**
```java
@Profile("dev")
@Configuration
public class DevConfig {
    // Beans specific to development environment
}
```

---

### 🔹 32. How to Check Environment Properties in Spring Boot?

You can use the **Environment** object to access environment properties and configuration values (from `.properties`, command-line, or environment variables).

✅ **Example:**
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;
import org.springframework.stereotype.Component;

@Component
public class EnvChecker {

    @Autowired
    private Environment env;

    public void printProperties() {
        System.out.println(env.getProperty("spring.datasource.url"));
        System.out.println(env.getActiveProfiles()[0]);
    }
}
```

---

### 🔹 33. How to Enable Debugging Logs in Spring Boot?

You can enable **debug-level logging** in Spring Boot to get more detailed logs.

#### ✅ Option 1 — application.properties
```properties
logging.level.root=DEBUG
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %msg%n
```

#### ✅ Option 2 — Command Line
```bash
java -jar app.jar --debug
```

#### ✅ Option 3 — Change Log Level at Runtime (using Actuator)
```bash
curl -X POST http://localhost:8080/actuator/loggers/<logger-name> \
-H "Content-Type: application/json" \
-d '{"configuredLevel": "DEBUG"}'
```

---

✅ **Summary**
| Concept | Purpose |
|----------|----------|
| **Profiles** | Define environment-specific configurations |
| **Environment** | Access app configuration and system properties |
| **Debug Logs** | Enable detailed logging for troubleshooting |

---
---

### Dependency Injection and IoC

## ⚙️ Spring Core Concepts — Dependency Injection & Beans

---

### 🔹 34. What is Dependency Injection (DI)?

**Dependency Injection (DI)** is a **design pattern** used in Spring to achieve **loose coupling** between objects.

Instead of an object creating its dependencies, they are **provided (injected)** by the Spring **IoC container**.

📘 **Advantages:**
- Increases reusability and testability  
- Reduces tight coupling between components  
- Simplifies object management  

#### ✅ Types of Dependency Injection:
1. **Constructor Injection**  
   - Dependencies are injected through the constructor.  
   ```java
   @Component
   public class Student {
       private final Course course;

       @Autowired
       public Student(Course course) {
           this.course = course;
       }
   }
   ```

2. **Setter Injection**  
   - Dependencies are injected through setter methods.  
   ```java
   @Component
   public class Student {
       private Course course;

       @Autowired
       public void setCourse(Course course) {
           this.course = course;
       }
   }
   ```

3. **Field Injection**  
   - Dependencies are injected directly into fields using `@Autowired`.  
   ```java
   @Component
   public class Student {
       @Autowired
       private Course course;
   }
   ```

---

### 🔹 35. What is an IoC (Inversion of Control) Container?

The **IoC Container** in Spring is responsible for:
- Creating, configuring, and managing the lifecycle of beans.
- Performing **Dependency Injection** automatically.

📦 **Common IoC Containers:**
- **BeanFactory** – Basic container with lazy loading.  
- **ApplicationContext** – Advanced container with extra features (like event handling, AOP support, etc.).

✅ **Example:**
```java
ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
MyService service = context.getBean(MyService.class);
```

---

### 🔹 36. Difference between Constructor and Setter Injection

| **Feature** | **Constructor Injection** | **Setter Injection** |
|--------------|----------------------------|----------------------|
| **Dependency Injection Method** | Through constructor parameters | Through setter methods |
| **Immutability** | Promotes immutability — dependencies fixed at creation | Allows mutable dependencies |
| **When Used** | When all dependencies are mandatory | When some dependencies are optional |
| **Overriding Dependencies** | Harder to override | Easier to override after object creation |

---

### 🔹 4. What is a Spring Bean?

A **Spring Bean** is any object that is **managed by the Spring IoC container**.  
Spring creates, initializes, and injects beans into other beans as required.

✅ **Example:**
```java
@Component
public class EmployeeService {
    // This is a Spring Bean managed by the container
}
```

---

### 🔹 5. What are Inner Beans in Spring?

**Inner Beans** are beans defined **within another bean’s configuration**.  
They are used when a bean is **only needed by one specific bean** and doesn’t need a global name.

✅ **Example (XML-based configuration):**
```xml
<bean id="student" class="com.example.Student">
    <property name="course">
        <bean class="com.example.Course"/>
    </property>
</bean>
```
Here, `Course` is an **Inner Bean** inside `Student`.

---

### 🔹 6. What is Bean Wiring?

**Bean Wiring** is the process of **connecting beans together** so that they can collaborate.  
It tells Spring **which beans depend on which other beans**.

🧩 **Two Types of Bean Wiring:**
1. **Autowiring:**  
   Spring automatically injects dependencies using annotations like `@Autowired`.

2. **Manual Wiring:**  
   Dependencies are defined explicitly in configuration (XML or Java-based).

✅ **Example:**
```java
@Configuration
public class AppConfig {
    @Bean
    public Engine engine() {
        return new Engine();
    }

    @Bean
    public Car car(Engine engine) {
        return new Car(engine);
    }
}
```

---

✅ **Summary**

| Concept | Description |
|----------|--------------|
| **Dependency Injection** | Pattern for injecting dependent objects automatically |
| **IoC Container** | Core mechanism managing bean lifecycle and DI |
| **Spring Bean** | Object managed by IoC container |
| **Inner Bean** | Bean defined within another bean’s configuration |
| **Bean Wiring** | Process of linking dependent beans |
| **Injection Types** | Constructor, Setter, Field |

---
---

### Spring Data JPA and Database

## 💾 Spring Data and Database Connectivity in Spring Boot

---

### 🔹 2. Explain Spring Data and What is Spring Data JPA?

**Spring Data** is a part of the larger Spring framework designed to simplify **data access layers** in applications.  
It provides a consistent, high-level abstraction for working with **different data sources** such as relational databases, NoSQL databases, and even cloud data stores.

📘 **Key Features:**
- Reduces boilerplate code for database operations  
- Provides repositories with built-in CRUD methods  
- Supports both SQL and NoSQL databases  
- Offers integration with JPA, MongoDB, Elasticsearch, and more  

---

### 🧩 **Spring Data JPA**

**Spring Data JPA** is a submodule of Spring Data that focuses on **JPA-based repositories** (Java Persistence API).  
It simplifies working with **relational databases** like MySQL, PostgreSQL, or H2 by abstracting away repetitive JPA boilerplate.

✅ **Example:**
```java
@Repository
public interface StudentRepository extends JpaRepository<Student, Long> {
    List<Student> findByName(String name);
}
```

Spring Data JPA automatically implements this repository at runtime, so developers can focus on business logic instead of SQL queries.

---

### 🔹 8. What Error Occurs if H2 is Not Present in the Classpath?

If the **H2 database driver** is missing from the classpath and Spring Boot attempts to auto-configure it, you’ll encounter the following error:

```
java.lang.ClassNotFoundException: org.h2.Driver
```

🛠 **Solution:**
Add the following dependency in your `pom.xml`:
```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

---

### 🔹 9. Steps to Connect a Spring Boot Application to a Database Using JDBC

To connect an external database (like **MySQL**, **PostgreSQL**, or **Oracle**) to Spring Boot using **JDBC**, follow these steps:

#### ✅ 1. Add Database Driver Dependency
For example, for MySQL:
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

#### ✅ 2. Configure `application.properties`
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

#### ✅ 3. Create a `JdbcTemplate` Bean
```java
@Configuration
public class JdbcConfig {
    @Autowired
    private DataSource dataSource;

    @Bean
    public JdbcTemplate jdbcTemplate() {
        return new JdbcTemplate(dataSource);
    }
}
```

#### ✅ 4. Use `JdbcTemplate` for Queries
```java
@Repository
public class EmployeeRepository {
    @Autowired
    private JdbcTemplate jdbcTemplate;

    public List<Employee> findAll() {
        return jdbcTemplate.query("SELECT * FROM employees",
                (rs, rowNum) -> new Employee(rs.getInt("id"), rs.getString("name")));
    }
}
```

---

### 🔹 11. What Do You Understand About Spring Data REST?

**Spring Data REST** is a project that **automatically exposes Spring Data repositories as RESTful APIs**.  
It uses the **Spring MVC** and **Spring HATEOAS** frameworks under the hood to convert your repository interfaces into REST endpoints — **without writing any controller code**.

✅ **Example:**
```java
@RepositoryRestResource
public interface ProductRepository extends JpaRepository<Product, Long> {}
```

This automatically exposes endpoints like:
```
GET /products
POST /products
GET /products/{id}
```

🧩 **Advantages:**
- Rapid API generation  
- Minimal configuration required  
- Automatically supports pagination, sorting, and filtering  

---

### 🔹 12. Why is Spring Data REST Not Recommended for Real-World Applications?

While **Spring Data REST** is useful for prototypes and small projects, it has **limitations** that make it less suitable for production-scale systems.

| **Limitation** | **Description** |
|-----------------|-----------------|
| **Performance Issues** | Not optimized for large-scale systems with complex queries. |
| **Versioning Challenges** | Difficult to manage API versioning over time. |
| **Complex Relationships** | Handling entity relationships (One-to-Many, Many-to-Many) becomes cumbersome. |
| **Limited Filtering** | Built-in filters are basic; advanced filtering requires custom code. |
| **Security Concerns** | Exposes repositories directly, increasing potential attack surface. |

🧠 **Better Approach:**  
Use **Spring Data JPA** with **Spring MVC controllers** to build customized, secured, and versioned REST APIs.

---
---



