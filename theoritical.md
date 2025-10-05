![Java Features](https://media.geeksforgeeks.org/wp-content/uploads/20240401182630/Features-of-Java-768.png)

---

# 📑 Table of Contents for Java Interview Questions

- [JVM & Fundamentals](#jvm--fundamentals)  
- [String Handling](#string-handling)  
- [OOP Concepts](#oop-concepts)  
- [Collections Framework (Core)](#collections-framework-core)  
- [Exception Handling](#exception-handling)  
- [Multithreading](#multithreading)  


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
---

### Collections Framework (Core)

🔹 What is the Java Collection Framework?

The Java Collection Framework (JCF) is a set of classes and interfaces that provide ready-made data structures and algorithms to store, manipulate, and access data efficiently.

---

# 🔹 Hierarchy of the Java Collection Framework

The **Java Collection Framework (JCF)** is organized into a **well-defined hierarchy** of interfaces and classes that represent different types of data structures.

At the top of the hierarchy lies the **`Iterable`** interface, which is the root for all collection classes (except Map).

---

## 🧩 Basic Structure

![Java Collection Framework Hierarchy](https://media.geeksforgeeks.org/wp-content/uploads/20250901105730206395/2.webp)


```
                 Iterable
                     |
                Collection
           /          |          \
         List        Set         Queue
                      \
                     SortedSet (NavigableSet)
```

And separately:

```
                    Map
                     |
                SortedMap (NavigableMap)
```

---

## 🔸 Explanation of Major Interfaces

### 1. **Iterable**
- Root interface for all collection classes.
- Provides the **`iterator()`** method to iterate over elements using enhanced for-loops.
- Example:  
  ```java
  for (int x : list) { ... }
  ```

---

### 2. **Collection**
- The root interface for all **List**, **Set**, and **Queue** types.
- Defines common operations like `add()`, `remove()`, `clear()`, `size()`, etc.

---

### 3. **List Interface**
- **Ordered collection**, allows **duplicate** elements.
- Elements can be **accessed by index**.
- **Implementations:**
  - `ArrayList` → dynamic array
  - `LinkedList` → doubly linked list
  - `Vector` → synchronized version of ArrayList
  - `Stack` → LIFO structure (extends Vector)

---

### 4. **Set Interface**
- **Unordered collection** that does **not allow duplicates**.
- **Implementations:**
  - `HashSet` → backed by a `HashMap`, unordered
  - `LinkedHashSet` → maintains insertion order
  - `TreeSet` → stores elements in sorted order (uses a Red-Black Tree)

---

### 5. **Queue Interface**
- Follows **FIFO (First In, First Out)** order.
- Used for scheduling or task queues.
- **Implementations:**
  - `PriorityQueue` → elements ordered by priority (min-heap by default)
  - `LinkedList` → can also act as a queue
  - `Deque` → double-ended queue (can be used as stack/queue)

---

### 6. **Map Interface**
- Stores elements as **key-value pairs**.
- Keys must be **unique**, values can be **duplicated**.
- Not a part of the `Collection` interface but belongs to the framework.
- **Implementations:**
  - `HashMap` → unordered
  - `LinkedHashMap` → insertion order
  - `TreeMap` → sorted order (by keys)
  - `Hashtable` → synchronized (legacy)
  - `ConcurrentHashMap` → thread-safe

---

## 🧠 Summary Table

| Interface | Allows Duplicates | Maintains Order | Key Implementations |
|------------|------------------|------------------|---------------------|
| **List** | ✅ Yes | ✅ Yes | ArrayList, LinkedList |
| **Set** | ❌ No | ⚠️ Some (LinkedHashSet) | HashSet, TreeSet |
| **Queue** | ⚠️ Depends | ✅ Yes | PriorityQueue, LinkedList |
| **Map** | ❌ Keys only | ⚠️ Some (LinkedHashMap) | HashMap, TreeMap |

---
---

# 🔹 ArrayList and Thread-Safety in Java

## Question:
How does **ArrayList** work internally in Java, how can it be **synchronized or made read-only**, how is it **converted to/from arrays**, and how does it **grow dynamically** compared to Vectors?

---

## Answer:

### 1. **Synchronization of ArrayList**
- **Collections.synchronizedList(list)**: Wraps an ArrayList to make it thread-safe.
- **CopyOnWriteArrayList**: Thread-safe variant of ArrayList suitable for concurrent reads and infrequent writes.

**Example:**
```java
List<Integer> syncList = Collections.synchronizedList(new ArrayList<>());
CopyOnWriteArrayList<Integer> cowList = new CopyOnWriteArrayList<>();
```

**Why ArrayList even though Vector exists?**
- ArrayList is **faster** than Vector.
- ArrayList supports **modern multithreading patterns**; Vector synchronizes each method individually, making it slower.
- Vector is **legacy** and mostly outdated.

---

### 2. **Memory Storage**
- **Array:** Contiguous memory block; direct index access via base address.
- **ArrayList:** Also uses contiguous memory; **dynamic resizing** occurs when capacity is full — a new, larger array is created and elements are copied over.

---

### 3. **Conversion Between Array and ArrayList**

**Array → ArrayList**
```java
String[] arr = {"A","B","C"};
List<String> list = Arrays.asList(arr);
```

**ArrayList → Array**
```java
List<Integer> list = new ArrayList<>(Arrays.asList(1,2,3));
Integer[] arr = list.toArray(new Integer[list.size()]);
```

---

### 4. **Dynamic Growth of ArrayList**
- Default capacity: ~10 (depends on Java version)
- When capacity is full:
  1. Create a new larger array.
  2. Copy all elements from old array.
  3. Use new array as internal storage.
- This process is called **resizing**.

---

### 5. **Making ArrayList Read-Only**
- Use `Collections.unmodifiableList(list)` to create a **read-only view**.
```java
List<Character> list = new ArrayList<>(Arrays.asList('X','Y','Z'));
List<Character> readOnlyList = Collections.unmodifiableList(list);
readOnlyList.add('A'); // Throws UnsupportedOperationException
```

---

# 🔹 LinkedList Class in Java

- **Definition:** `LinkedList` in Java is a class that implements a **doubly linked list** to store elements.
- **Inheritance & Interfaces:**  
  Inherits from `AbstractList` and implements **List** and **Deque** interfaces.
- **Key Properties:**
  - Non-synchronized (not thread-safe by default)
  - Maintains **insertion order**
  - Can be used as a **List**, **Stack**, or **Queue**
- **Syntax:**
```java
LinkedList<Type> list_name = new LinkedList<Type>();
```
- **Use cases:**  
  Efficient insertion/deletion at any position; when frequent add/remove operations are required.

---

# 🔹 Stack Class in Java

- **Definition:** `Stack` is a **LIFO (Last In First Out)** data structure derived from the `Vector` class with stack-specific methods.
- **Common Methods:**
  | Method | Description |
  |--------|-------------|
  | `peek()` | Returns the top element without removing it |
  | `empty()` | Checks if the stack is empty (true/false) |
  | `push(E item)` | Adds an element to the top of the stack |
  | `pop()` | Removes and returns the top element |
  | `search(Object o)` | Returns the 1-based position from the top; -1 if not found |

- **Use cases:** Undo operations, expression evaluation, recursion simulation, backtracking problems.

---

# 🔹 Set Interface in Java

- **Definition:** `Set` is a collection that **does not allow duplicate elements**.
- **Key Properties:**
  - No duplicates
  - No guaranteed ordering (depends on implementation)
- **Common Implementations:**
  | Class | Description |
  |-------|-------------|
  | `HashSet` | Stores elements in a **hash table**; unordered; fast lookup and insertion |
  | `LinkedHashSet` | Maintains **insertion order** while using a hash table |
  | `TreeSet` | Stores elements in **sorted order** using natural ordering or a custom comparator |

---

# 🔹 HashSet Class in Java

- **Definition:** `HashSet` implements the **Set** interface and stores a collection of **distinct elements**.
- **Internal Storage:**
  - Uses a **hash table**.
  - Each element is mapped to an **index (bucket)** using a hash function.
  - Lookup, insertion, and deletion are **O(1)** on average, assuming good hash distribution.
- **Key Properties:**
  - No duplicates
  - No guaranteed order
  - Provides **constant-time performance** for `add()`, `remove()`, `contains()`, and `size()`.
- **Use cases:** Efficient membership checking, storing unique elements, eliminating duplicates.

---


# 🔹 ConcurrentHashMap in Java

- **Definition:** A thread-safe variant of HashMap that allows concurrent read and write operations without locking the entire map.
- **Implementation:** Internally based on **segment locks** (bucket-level locking) similar to Hashtable, allowing high concurrency.
- **Syntax:**
```java
public class ConcurrentHashMap<K, V> 
    extends AbstractMap<K, V> 
    implements ConcurrentMap<K, V>, Serializable
```
- **Parameters:**  
  `K` → Key type, `V` → Value type
- **Use cases:** Multi-threaded environments where multiple threads read and write frequently.

---

# 🔹 Difference between Collection and Collections

| Feature | Collection | Collections |
|---------|------------|------------|
| Type | Interface | Class |
| Purpose | Defines standard data structure functionality | Provides utility methods like sort, reverse, synchronization |
| Methods | Instance methods for data structures | Static methods for operations on collections |

---

# 🔹 Difference between Array and ArrayList

| Feature | Array | ArrayList |
|---------|-------|-----------|
| Dimensions | Single or multi-dimensional | Single-dimensional |
| Traversal | for / foreach loop | Iterator |
| Size | Fixed | Dynamic (can grow or shrink) |
| Performance | Faster (fixed size) | Slower (dynamic resizing overhead) |
| Primitives | Directly stored | Requires autoboxing/unboxing |
| Type Safety | Less type-safe | Type-safe with generics |
| Adding Elements | Using assignment operator | Using `add()` method |

---

# 🔹 Difference between ArrayList and LinkedList

| Feature | ArrayList | LinkedList |
|---------|-----------|------------|
| Implementation | Resizable array | Doubly linked list |
| Memory Storage | Contiguous memory | Non-contiguous memory (nodes with references) |
| Random Access | Fast | Slow |
| Insertion/Deletion | Slower | Faster |
| Memory Efficiency | More memory efficient | Less memory efficient (extra references) |
| Searching | Faster | Slower |

---

# 🔹 Difference between ArrayList and Vector

| Feature | ArrayList | Vector |
|---------|-----------|--------|
| Implementation | Resizable array | Synchronized resizable array |
| Synchronization | Not synchronized | Synchronized |
| Performance | Faster (single-threaded) | Slower due to synchronization overhead |
| Introduced | Java 1.2 | JDK 1.0 |
| Recommended Use | Single-threaded | Multi-threaded |
| Default Capacity | 10 | 10 (double on expansion) |

---

# 🔹 Difference between HashMap and Hashtable

| Feature | HashMap | Hashtable |
|---------|---------|----------|
| Synchronization | Not synchronized | Synchronized |
| Null Keys/Values | One null key, multiple null values | Not allowed |
| Traversal | Iterator | Iterator and Enumerator |
| Performance | Faster | Slower |

---

# 🔹 Difference between Set and Map

| Feature | Set | Map |
|---------|-----|-----|
| Inheritance | Extends Collection interface | Does not extend Collection |
| Duplicates | Not allowed | Values can be duplicated; keys unique |
| Nulls | One null element | Multiple null values allowed for values, one null key |
| Purpose | Collection of unique elements | Key-value pairs storage |

---
---

### Exception Handling

# ☕ Java Exception Handling — Complete Notes

---

## 🔹 What is Exception Handling?

An **Exception** in Java is an **event that interrupts the normal flow** of program execution and requires special handling.  
The **Java Exception Handling mechanism** allows developers to manage runtime errors gracefully, preventing abrupt program termination.

### ⚙️ Common Causes of Exceptions
- Device failure  
- Loss of network connection  
- Code errors  
- Opening an unavailable file  
- Invalid user input  
- Physical limitations (e.g., out of memory)

---

## 🔹 Types of Exceptions in Java

Java exceptions are broadly classified into two categories:

### 1. **Built-in Exceptions**
Provided by Java libraries, these are predefined and can be further divided into:

#### ✅ Checked Exceptions
Handled **during compile-time**. The compiler ensures these are either caught or declared using `throws`.
- `IOException`
- `FileNotFoundException`
- `ClassNotFoundException`
- `InterruptedException`

#### ⚠️ Unchecked Exceptions
Handled **during runtime** (not checked by compiler). Usually occur due to programming mistakes.
- `NullPointerException`
- `ArrayIndexOutOfBoundsException`
- `ArithmeticException`
- `RuntimeException`

### 2. **User-Defined Exceptions**
Created by programmers for handling specific cases not covered by built-in exceptions.  
Defined by extending the `Exception` class.

```java
class MyCustomException extends Exception {
    public MyCustomException(String message) {
        super(message);
    }
}
```

---

## 🔹 Difference Between Error and Exception

| **Aspect** | **Errors** | **Exceptions** |
|-------------|-------------|----------------|
| **Recoverability** | Cannot be recovered from | Can be handled or recovered using `try-catch` or `throws` |
| **Type** | Always unchecked | Can be checked or unchecked |
| **Cause** | Environment-related (JVM issues) | Program-related (logic or runtime issues) |
| **When Occur** | Compile-time or runtime | Runtime (checked known to compiler) |
| **Package** | `java.lang.Error` | `java.lang.Exception` |
| **Examples** | `StackOverflowError`, `OutOfMemoryError` | Checked: `IOException`, `SQLException` <br> Unchecked: `NullPointerException`, `ArithmeticException` |

---

## 🔹 Hierarchy of Exception Classes

All exception and error types in Java are subclasses of the **`Throwable`** class.  

```
               Object
                  │
              Throwable
              ┌────────┐
              │        │
           Exception   Error
           ┌──────┐
           │      │
  Checked Exceptions  Unchecked (Runtime) Exceptions
```

### Key Points:
- `Throwable` → Base class for all exceptions and errors.
- `Exception` → Represents issues that programs should handle.
- `Error` → Represents serious system failures (JVM related).

📌 Example:
- `NullPointerException` → Subclass of `RuntimeException` → Subclass of `Exception`
- `StackOverflowError` → Subclass of `Error`

---

## 🔹 Runtime Exceptions (Unchecked)

**Runtime Exceptions** occur **during program execution**.  
They are **not checked by the compiler** and usually indicate programming mistakes.

### ✴️ Common Runtime Exceptions
- **`NullPointerException`** → Using an object reference that is `null`.  
- **`ArrayIndexOutOfBoundsException`** → Accessing array index beyond valid range.  
- **`ArithmeticException`** → Division by zero or invalid arithmetic.  
- **`IllegalArgumentException`** → Passing invalid or inappropriate argument to a method.  

### 💡 Key Points:
- Do **not** require `throws` declaration.
- Should still be handled with `try-catch` to prevent crashes.
- Help identify logical and coding errors quickly.

---

## 🔹 NullPointerException (NPE)

`NullPointerException` is a **runtime exception** thrown when:
- You try to **access or modify** an object reference that is `null`.

### 🧠 Example:
```java
String str = null;
System.out.println(str.length()); // Throws NullPointerException
```

### ✅ Prevention Tips:
- Always check if an object is `null` before use.
- Use **Optional** (Java 8+) to handle nullable objects.
- Initialize objects properly before accessing them.

---
---

# ☕ Java Exception Handling — Keywords and Custom Exceptions

---

## 🔹 1. try

The `try` block contains code that **might throw an exception**.  
It must be followed by **catch** or **finally** block.

```java
try {
    int result = 10 / 0; // may throw ArithmeticException
} 
```

---

## 🔹 2. catch

The `catch` block is used to **handle exceptions** thrown by the `try` block.  
You can have **multiple catch blocks** to handle different exception types.

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero: " + e.getMessage());
}
```

---

## 🔹 3. finally

The `finally` block is **always executed**, regardless of whether an exception occurs or not.  
It is typically used for **resource cleanup** (e.g., closing files, DB connections).

```java
try {
    int result = 10 / 2;
} catch (ArithmeticException e) {
    System.out.println("Exception caught");
} finally {
    System.out.println("This always executes");
}
```

---

## 🔹 4. throw

The `throw` keyword is used to **explicitly throw an exception** from a method or block.

```java
public void checkAge(int age) {
    if (age < 18) {
        throw new ArithmeticException("Age must be 18 or above");
    }
}
```

---

## 🔹 5. throws

The `throws` keyword is used in a **method signature** to declare the exceptions it might throw.  
It informs the **caller** that they must handle or propagate these exceptions.

```java
public void readFile(String fileName) throws IOException {
    FileReader file = new FileReader(fileName);
    file.read();
}
```

---

## 🔹 6. Custom Exceptions (User-Defined)

Custom exceptions allow you to **define your own exception types** for specific scenarios.

```java
// Define a custom exception
class MyCustomException extends Exception {
    public MyCustomException(String message) {
        super(message);
    }
}

// Use custom exception
public class Main {
    public static void validate(int number) throws MyCustomException {
        if (number < 0) {
            throw new MyCustomException("Number must be non-negative");
        }
    }

    public static void main(String[] args) {
        try {
            validate(-5);
        } catch (MyCustomException e) {
            System.out.println("Custom Exception caught: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Custom Exception caught: Number must be non-negative
```

---
---

### Multithreading

# ☕ Java Multithreading & Concurrency — Core Concepts

---

## 🔹 What is Multithreading?

**Multithreading** in Java allows the **concurrent execution** of two or more parts of a program to make efficient use of CPU.  
Each part of such a program is called a **thread**, and all threads share the same memory space.

---

## 🔹 Creating Threads in Java

There are **two primary ways** to create threads in Java:

### 1. Extending the `Thread` Class
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running using Thread class.");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();  // starts the thread and calls run()
    }
}
```

### 2. Implementing the `Runnable` Interface
```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread running using Runnable interface.");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable());
        t1.start();
    }
}
```

> ✅ Prefer **Runnable** over **Thread inheritance** when your class needs to extend another class (since Java supports single inheritance only).

---

## 🔹 Thread Lifecycle

A thread in Java goes through the following **stages**:

1. **New** → Thread created but not started (`Thread t = new Thread()`).
2. **Runnable** → Thread is ready to run but waiting for CPU time (`t.start()`).
3. **Running** → Thread is currently executing its `run()` method.
4. **Blocked / Waiting** → Thread temporarily inactive, waiting for a monitor lock or signal.
5. **Terminated (Dead)** → Thread has completed its execution or stopped due to an error.

---

## 🔹 Synchronization

When multiple threads access shared data, **race conditions** can occur.  
**Synchronization** ensures that only one thread accesses a resource at a time.

### Using `synchronized` keyword
```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

> The `synchronized` keyword locks the method or block so only one thread can execute it at a time.

---

## 🔹 volatile Keyword

The `volatile` keyword ensures that changes to a variable are **immediately visible** to all threads.  
It prevents threads from caching variables locally.

```java
volatile boolean flag = true;
```

> Used for lightweight synchronization where atomicity is not required.

---

## 🔹 Thread Communication — wait(), notify(), notifyAll()

Used when multiple threads **share resources** and need to **communicate** with each other.

- `wait()` — thread releases the lock and waits.
- `notify()` — wakes up one waiting thread.
- `notifyAll()` — wakes up all waiting threads.

```java
class Shared {
    synchronized void printMessage() throws InterruptedException {
        wait();  // waits for notify()
        System.out.println("Thread resumed");
    }

    synchronized void trigger() {
        notify();  // wakes waiting thread
    }
}
```

---

## 🔹 sleep() Method

`Thread.sleep(milliseconds)` pauses the current thread for the specified time.

```java
Thread.sleep(1000); // pauses for 1 second
```

---

## 🔹 Thread Safety Basics

A class is **thread-safe** if it behaves correctly when accessed by multiple threads simultaneously.

✅ Tips for thread safety:
- Use **synchronized** methods or blocks.
- Prefer **immutable** objects.
- Use **atomic classes** (e.g., `AtomicInteger`, `AtomicBoolean`).
- Use concurrent collections like `ConcurrentHashMap`.

---

## 🔹 ConcurrentHashMap

`ConcurrentHashMap` is a **thread-safe version of HashMap** that allows **concurrent reads** and **controlled writes** without locking the entire map.

### Features:
- Concurrent read operations.
- Partial locking (only segments, not entire map).
- No `ConcurrentModificationException`.

### Example:
```java
import java.util.concurrent.ConcurrentHashMap;

public class Main {
    public static void main(String[] args) {
        ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();
        map.put(1, "Java");
        map.put(2, "Python");

        System.out.println(map.get(1)); // Output: Java
    }
}
```

---

## ✅ Summary Table

| Concept | Description |
|----------|--------------|
| **Thread creation** | `extends Thread` or `implements Runnable` |
| **Lifecycle** | New → Runnable → Running → Waiting → Terminated |
| **Synchronization** | Prevents concurrent data corruption |
| **volatile** | Ensures variable visibility between threads |
| **wait/notify** | Thread communication |
| **sleep()** | Pause execution |
| **Thread safety** | Ensures consistent behavior under concurrency |
| **ConcurrentHashMap** | Thread-safe, high-performance map |

---
---

