![Java Features](https://media.geeksforgeeks.org/wp-content/uploads/20240401182630/Features-of-Java-768.png)

---

# 📑 Table of Contents for Java Interview Questions

- [JVM & Fundamentals](#jvm--fundamentals)  
- [String Handling](#string-handling)  
- [OOP Concepts](#oop-concepts)  
- [Collections Framework (Core)](#collections-framework-core)  
- [Exception Handling](#exception-handling)  


---
---

### JVM & Fundamentals

## 1. Is Java Platform Independent? If yes, how?

Yes, **Java is a platform-independent language**. Unlike many programming languages, `javac` compiles the program into a **bytecode (`.class` file)** instead of native machine code.  

- This bytecode is **independent of the operating system and hardware**.  
- However, it requires a **JVM (Java Virtual Machine)** installed on the target machine to execute the bytecode.  
- Although JVM itself is platform-dependent, the **bytecode remains the same across all platforms**, which makes Java platform independent.  

**Key Point**:  
- Write once, run anywhere (WORA) is possible because of Java bytecode + JVM.  

---

## 3. What is JVM?

JVM stands for **Java Virtual Machine**. It is a **part of the JRE** and acts as an interpreter for Java bytecode.  

**Responsibilities of JVM**:  
- Loading `.class` files (bytecode).  
- Verifying the bytecode for security and correctness.  
- Executing the bytecode (either by interpretation or JIT compilation).  
- Providing runtime memory management and garbage collection.  

**Important Notes**:  
- JVM is platform-dependent (different implementations exist for Windows, Linux, macOS).  
- JVM makes Java *platform-independent* by executing the same bytecode on any OS.  

![JVM Diagram](https://media.geeksforgeeks.org/wp-content/uploads/20240401182730/JVM-768.png)

---

## 4. What is JIT?

JIT stands for **Just-In-Time Compiler**, which is a part of the JVM.  
It improves the performance of Java applications by compiling bytecode into **native machine code at runtime**, instead of interpreting it line by line.  

**How JIT Works**:  
1. Source code → compiled using `javac` → bytecode (`.class` file).  
2. JVM loads the bytecode.  
3. JIT compiler compiles frequently used methods into **native machine code**.  
4. JVM executes the compiled code directly instead of interpreting it repeatedly.  

**Advantages of JIT**:  
- Faster execution of frequently used code.  
- Optimizations at runtime.  
- Better performance compared to pure interpretation.  

![JIT Diagram](https://media.geeksforgeeks.org/wp-content/uploads/20240401182857/JIT-768.png)

---

## 5. What are the Memory Storages available in JVM?

The JVM consists of several memory areas used during program execution:  

1. **Class (Method) Area**  
   - Stores class-level data such as runtime constant pool, field & method data, and bytecode.  

2. **Heap**  
   - Stores all Java objects and arrays.  
   - Shared among all threads.  

3. **Stack**  
   - Stores method call information, local variables, and partial results.  
   - Each thread has its own stack.  

4. **Program Counter (PC) Register**  
   - Stores the address of the JVM instruction currently being executed.  

5. **Native Method Stack**  
   - Stores native (non-Java) method information.  

![JVM Memory Areas](https://media.geeksforgeeks.org/wp-content/uploads/20240402092041/JVM-Areas-768.png)

---

## 6. What is a ClassLoader?

A **ClassLoader** is a part of the JRE that loads Java classes into the JVM during runtime.  
It dynamically loads `.class` files into memory whenever required.  

**Types of ClassLoaders**:  
1. **Bootstrap ClassLoader** – Loads core Java classes (`java.lang.*`, `java.util.*`).  
2. **Extension ClassLoader** – Loads classes from `ext` directory (`javax.*`).  
3. **Application ClassLoader** – Loads user-defined classes from the classpath.  

**Key Point**:  
- ClassLoader removes the need for JVM to know about the file system.  

---

## 7. Difference between JVM, JRE, and JDK

| Feature | JVM | JRE | JDK |
|---------|-----|-----|-----|
| Full Form | Java Virtual Machine | Java Runtime Environment | Java Development Kit |
| Purpose | Executes bytecode | Provides environment to run Java apps | Provides tools to develop + run Java apps |
| Includes | Interpreter, JIT, GC | JVM + libraries + other files | JRE + compiler (`javac`) + dev tools |
| Platform Dependency | Yes | Yes | Yes |

**In short**:  
- **JVM**: The engine that executes bytecode.  
- **JRE**: JVM + runtime libraries (to run Java apps).  
- **JDK**: JRE + development tools (to develop and run apps).  

---
---

### String Handling

## 10. What is Java String Pool?

The **Java String Pool** is a special memory area inside the **heap** where Java stores string literals.  
- When a new string is created, JVM first checks the pool.  
- If it exists, the same reference is reused.  
- If not, a new object is created in the pool.  

This mechanism saves memory and improves performance.

**Example:**
```java
String str1 = "Hello";  
// "Hello" will be stored in the String Pool  
// str1 will point to the pool reference
```

**Image:**  
![Java String Pool](https://media.geeksforgeeks.org/wp-content/uploads/20240402092413/Java-String-Pool-768.png)

---

## Comparison: String vs StringBuffer vs StringBuilder

| Feature          | String                                        | StringBuffer                                   | StringBuilder                                   |
|------------------|-----------------------------------------------|------------------------------------------------|-------------------------------------------------|
| Nature           | Immutable (cannot be changed after creation)  | Mutable (contents can be changed)              | Mutable (contents can be changed)               |
| Storage Location | String Pool (for literals), Heap (for new)    | Heap                                           | Heap                                            |
| Thread-safety    | Not thread-safe                               | Thread-safe (methods synchronized)             | Not thread-safe                                 |
| Performance      | Fast for fixed data (no modification)         | Slower due to synchronization                  | Faster (no synchronization overhead)            |
| Use-case         | Constant/fixed string values                  | Frequent modifications in multi-threaded code  | Frequent modifications in single-threaded code  |
| Memory Usage     | May create many objects if modified often     | Efficient for modifications (single object)    | Efficient for modifications (single object)     |
| Methods          | Many (concat, substring, etc.)                | append, insert, delete, reverse, etc.          | append, insert, delete, reverse, etc.           |
| Example          | `String s = "Hello";`                         | `StringBuffer sb = new StringBuffer("Hello");` | `StringBuilder sb = new StringBuilder("Hello");`|
| Modification     | Creates new object on modification            | Modifies current object                        | Modifies current object                         |

---

## Thread safety means that the methods of a class are designed so that multiple threads can access and modify an object concurrently without causing problems (like data corruption, unexpected results, or crashes).
---


### Example Code

**String Example (Immutable)**
```java
String str = "Hello";
str = str + " World"; // Creates a new String object
System.out.println(str); // Output: Hello World
```

**StringBuffer Example (Mutable & Thread-safe)**
```java
StringBuffer sb = new StringBuffer("Hello");
sb.append(" World"); // Modifies the same object
System.out.println(sb); // Output: Hello World
```

**StringBuilder Example (Mutable & NOT Thread-safe)**
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // Modifies the same object
System.out.println(sb); // Output: Hello World
```

---
## 49. Which among StringBuilder or StringBuffer should be preferred when there are a lot of updates?

- **String** is immutable → inefficient for frequent updates.  
- Use **StringBuffer** if **thread-safety** is required.  
- Use **StringBuilder** if **performance** is a priority in a **single-threaded** environment.  

---

## 50. Why is StringBuffer called mutable?

The **StringBuffer** class represents a changeable sequence of characters.  
Unlike **String**, it allows modification without creating new objects, making it **mutable**.

**Example:**
```java
// Java Program to demonstrate StringBuffer mutability
public class StringBufferExample {
    public static void main(String[] args) {
        StringBuffer s = new StringBuffer();
        s.append("Geeks");
        s.append("for");
        s.append("Geeks");
        String message = s.toString();
        System.out.println(message);
    }
}
```
---

## 51. How is the creation of a String using `new()` different from that of a literal?

- **String literal**: Stored in the **String Pool**. Reused if the same string exists.  
- **String using `new()`**: Always creates a new object in **heap memory**, even if the same content already exists in the pool.  

**Syntax:**
```java
String x = new String("ABC"); // stored in heap, not reused from pool
```

**Image:**  
![String new() vs literal](https://media.geeksforgeeks.org/wp-content/uploads/20240402093121/3-768.png)


---
---



