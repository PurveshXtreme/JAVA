![java]([https://media.geeksforgeeks.org/wp-content/uploads/20240401182730/JVM-768.png](https://media.geeksforgeeks.org/wp-content/uploads/20240401182630/Features-of-Java-768.png))

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

