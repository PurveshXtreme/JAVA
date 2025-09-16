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

### OOP Concepts

## 61. What is an Object-Oriented Paradigm?

A **paradigm** is a pattern or a method. Programming paradigms are approaches to solving problems and include:
- Imperative
- Logical
- Functional
- Object-Oriented

**Object-oriented paradigm** uses objects as base entities. Methods are applied on these objects, and concepts like encapsulation and inheritance are performed.  
> When programming revolves around objects and their interactions, it's called the object-oriented paradigm.

---

## 62. What are the Main Concepts of OOPs in Java?

- **Inheritance**
- **Polymorphism**
- **Abstraction**
- **Encapsulation**

---

## 63. Difference between Object-Oriented and Object-Based Programming Languages

| Object-Oriented Programming Language            | Object-Based Programming Language                   |
|------------------------------------------------|----------------------------------------------------|
| Covers concepts like inheritance, polymorphism, abstraction | Limited to objects and encapsulation              |
| Supports all built-in objects                  | Doesn't support all built-in objects                |
| Examples: Java, C#                             | Examples: JavaScript, Visual Basic                  |

---

## 70. What is an Object?

An **object** is a real-life entity with properties and methods.  
- It's an instance of a class.
- Declared using the `new` keyword.

---

## 74. What is a Constructor?

A **constructor** is a special method used to initialize objects.  
- Called when an object is created.
- The constructor's name is the same as the class.

**Example:**
```java
// Class Created
class XYZ {
    private int val;

    // Constructor
    XYZ(){
        val = 0;
    }
}
```

---

## 75. What Happens If You Don't Provide a Constructor in a Class?

If no constructor is provided, Java compiler **automatically generates a default constructor** with no arguments and no operation.

---

## 76. Types of Constructors in Java

1. **Default Constructor**:  
   Does not accept any parameters.  
   Used to set initial values for object attributes.  
   ```java
   class_Name();
   // Default constructor called
   ```

2. **Parameterized Constructor**:  
   Accepts parameters as arguments to assign values during initialization.  
   ```java
   class_Name(parameter1, parameter2, ...);
   // Values assigned to instance variables
   ```

---

## 77. Purpose of a Default Constructor

Constructors create instances of a class (objects).  
A **default constructor** does not accept parameters, so whatever values are assigned to object properties are considered default values.

---

## 78. What is a Copy Constructor in Java?

A **copy constructor** passes another object as a parameter so the properties of both objects are the same.  
> It creates a copy of an object using another object.

---

## 79. Where and How Can You Use a Private Constructor?

A **private constructor** prevents other classes from instantiating the object or subclassing.  
Commonly used in the **Singleton pattern**.

**Example:**
```java
// Java program to demonstrate Singleton pattern with private constructor
class GFG {
    static GFG instance = null;
    public int x = 10;

    // Private constructor can't be accessed outside the class
    private GFG() {}

    // Factory method to provide instances
    static public GFG getInstance() {
        if (instance == null)
            instance = new GFG();
        return instance;
    }
}
// Driver Class
class Main {
    public static void main(String args[]) {
        GFG a = GFG.getInstance();
        GFG b = GFG.getInstance();
        a.x = a.x + 10;
        System.out.println("Value of a.x = " + a.x);
        System.out.println("Value of b.x = " + b.x);
    }
}
```
**Output:**
```
Value of a.x = 20
Value of b.x = 20
```

---

## 80. Differences Between Constructors and Methods

| Constructors                                    | Methods                                     |
|-------------------------------------------------|---------------------------------------------|
| Called only when object is created              | Can be called multiple times                |
| No return type                                  | Has a return type (void or another type)    |
| Used to set up initial state                    | Used to perform specific actions            |

---

## 81. What is an Interface?

An **interface** in Java is a collection of static final variables and abstract methods that define a contract for classes.  
- Any class that implements an interface must implement its methods.
- Specifies **what** a class should do, not **how**.

**Syntax:**
```java
interface InterfaceName {
    // constant fields
    // methods (abstract by default)
}
```

**Example:**
```java
// Java Program to demonstrate Interface
interface Shape {
    double getArea();
    double getPerimeter();
}
class Circle implements Shape {
    private double radius;
    public Circle(double radius) { this.radius = radius; }
    public double getArea() {
        return Math.PI * radius * radius;
    }
    public double getPerimeter() {
        return 2 * Math.PI * radius;
    }
}
class GFG {
    public static void main(String[] args) {
        Circle circle = new Circle(5.0);
        System.out.println("Area of circle is " + circle.getArea());
        System.out.println("Perimeter of circle is " + circle.getPerimeter());
    }
}
```
**Output:**
```
Area of circle is 78.53981633974483
Perimeter of circle is 31.41592653589793
```
---

# OOPs Java Concepts – Notes

## 81. What is an Interface?

An **interface** in Java is a collection of static final variables and abstract methods that define the contract or agreement for a set of linked classes. Any class that implements an interface is required to implement a specific set of methods. It specifies the behavior that a class must exhibit but not the specifics of how it should be implemented.

**Syntax:**
```java
interface InterfaceName {
    // constant fields
    // methods that are abstract by default
}
```

---

## 84. Differences Between Abstract Class and Interface

| Abstract Class                                   | Interface                                      |
|--------------------------------------------------|------------------------------------------------|
| Both abstract and non-abstract methods may be found in an abstract class. | The interface contains only abstract methods (Java 7 and below; Java 8+ supports default/static methods). |
| Abstract Class supports final methods.           | The interface class does not support final methods. |
| Multiple inheritance is not supported by the abstract class. | Multiple inheritance is supported by interface class. |
| `abstract` keyword is used to declare an abstract class. | `interface` keyword is used to declare the interface class. |
| `extends` keyword is used to extend an abstract class. | `implements` keyword is used to implement the interface. |
| Abstract class can have members like `protected`, `private`, etc. | All interface members are `public` by default. |

---

## 89. What is the ‘IS-A’ Relationship in OOPs Java?

- ‘**IS-A**’ is a type of relationship where one class inherits from another class.  
- It represents inheritance.  
- Example: `Dog IS-A Animal` (Dog extends Animal).
- This relationship allows a subclass to be treated as an instance of its superclass.

**Other OOPs Relationships:**
- **HAS-A (Composition/Aggregation):** One class contains a reference to another class.  
  Example: `Car HAS-A Engine`.
- **Uses-A:** When a class uses another class for some operation, usually as a method parameter.

---

## 107. Can We Overload the main() Method?

Yes, in Java we can overload the `main()` method.  
- The JVM always calls the signature `public static void main(String[] args)` to start execution.
- However, you can define other `main()` methods with different parameter lists in the same class.
- These overloaded methods can be called from the standard main method.

**Example:**
```java
public class MainOverload {
    public static void main(String[] args) {
        System.out.println("Standard main method");
        main("Overloaded main");
    }

    public static void main(String arg) {
        System.out.println(arg);
    }
}
```

---
