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
---

