# Java Coding Round Interview Questions

**Reference:** [W3Schools Java How-To Guide](https://www.w3schools.com/java/java_howtos.asp)

---

## 📋 Table of Contents

- [OOPs Concepts](#oops-concepts)
- [Exception Handling](#exception-handling)
- [Multithreading](#multithreading)
- [Collections Framework](#collections-framework)
- [File Handling & I/O](#file-handling--io)
- [String Manipulation](#string-manipulation)
- [Important Concepts](#important-concepts)

---

## OOPs Concepts

### 1. Class & Object with Methods

**Question:** Create a `Student` class with fields and methods to display details and calculate grade.

```java
class Student {
    int id;
    String name;
    double marks;

    void setDetails(int id, String name, double marks) {
        this.id = id;
        this.name = name;
        this.marks = marks;
    }

    void display() {
        System.out.println("ID: " + id + ", Name: " + name + ", Marks: " + marks);
    }

    char getGrade() {
        if (marks >= 90) return 'A';
        else if (marks >= 75) return 'B';
        else if (marks >= 60) return 'C';
        else return 'D';
    }
}
```

---

### 2. Inheritance & Method Overriding

**Question:** Implement inheritance with parent `Vehicle` and child classes `Car` and `Bike`.

```java
class Vehicle {
    void start() {
        System.out.println("Vehicle starting...");
    }
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car starts with push button");
    }
}

class Bike extends Vehicle {
    @Override
    void start() {
        System.out.println("Bike starts with kick");
    }
}
```

---

### 3. Polymorphism (Overloading & Overriding)

**Question:** Demonstrate compile-time and runtime polymorphism.

```java
class Calculator {
    // Method Overloading
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}

class AdvancedCalculator extends Calculator {
    // Method Overriding
    @Override
    int add(int a, int b) {
        return a + b + 10;
    }
}
```

---

### 4. Abstraction (Abstract Class)

**Question:** Create abstract class `Shape` with concrete implementations.

```java
abstract class Shape {
    abstract double area();
}

class Circle extends Shape {
    double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    double area() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    double length, breadth;

    Rectangle(double l, double b) {
        this.length = l;
        this.breadth = b;
    }

    double area() {
        return length * breadth;
    }
}
```

---

### 5. Encapsulation (Getters & Setters)

**Question:** Create class with private fields and public getters/setters.

```java
class Employee {
    private int id;
    private String name;
    private double salary;

    public int getId() { return id; }
    public void setId(int id) { 
        if (id > 0) this.id = id; 
    }

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public double getSalary() { return salary; }
    public void setSalary(double salary) { 
        if (salary >= 0) this.salary = salary; 
    }
}
```

---

### 6. Constructor Overloading & Chaining

**Question:** Demonstrate constructor chaining using `this()`.

```java
class Student {
    String name;
    int age;
    String course;

    Student() {
        this("Unknown", 18, "Not Assigned");
    }

    Student(String name) {
        this(name, 18, "Computer Science");
    }

    Student(String name, int age, String course) {
        this.name = name;
        this.age = age;
        this.course = course;
    }

    void display() {
        System.out.println(name + " | " + age + " | " + course);
    }
}
```

---

## Exception Handling

### 1. Basic Try-Catch-Finally

**Question:** Handle division by zero exception.

```java
public class DivisionExample {
    public static void main(String[] args) {
        int a = 10, b = 0;
        try {
            int result = a / b;
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("Error: Division by zero!");
        } finally {
            System.out.println("Execution completed.");
        }
    }
}
```

---

### 2. Multiple Catch Blocks

**Question:** Handle multiple exceptions in order.

```java
public class MultipleCatch {
    public static void main(String[] args) {
        try {
            int[] arr = {10, 20, 30};
            int result = arr[5] / 0;
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Error: Invalid array index!");
        } catch (ArithmeticException e) {
            System.out.println("Error: Division by zero!");
        }
    }
}
```

---

### 3. Custom Exception

**Question:** Create and throw custom exception for age validation.

```java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public class CustomExceptionDemo {
    static void checkAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be 18 or above");
        }
        System.out.println("Valid age!");
    }

    public static void main(String[] args) {
        try {
            checkAge(16);
        } catch (InvalidAgeException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

---

## Multithreading

### 1. Thread Creation (Two Ways)

**Using extends Thread:**
```java
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Thread: " + i);
        }
    }
}
// Usage: new MyThread().start();
```

**Using implements Runnable:**
```java
class MyRunnable implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Runnable: " + i);
        }
    }
}
// Usage: new Thread(new MyRunnable()).start();
```

---

### 2. Synchronization

**Question:** Prevent race condition using synchronized method.

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

public class SyncExample {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) counter.increment();
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) counter.increment();
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Count: " + counter.getCount());
    }
}
```

---

### 3. Producer-Consumer Problem

**Question:** Implement inter-thread communication using wait() and notify().

```java
class SharedResource {
    private int data;
    private boolean hasData = false;

    public synchronized void produce(int value) throws InterruptedException {
        while (hasData) {
            wait();
        }
        this.data = value;
        hasData = true;
        System.out.println("Produced: " + data);
        notify();
    }

    public synchronized int consume() throws InterruptedException {
        while (!hasData) {
            wait();
        }
        hasData = false;
        System.out.println("Consumed: " + data);
        notify();
        return data;
    }
}
```

---

## Collections Framework

### 1. ArrayList vs HashSet

**Question:** Demonstrate List (allows duplicates) vs Set (unique elements).

```java
import java.util.*;

public class ListSetExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Python");
        list.add("Java");
        System.out.println("List: " + list); // [Java, Python, Java]

        Set<String> set = new HashSet<>(list);
        System.out.println("Set: " + set); // [Java, Python]
    }
}
```

---

### 2. HashMap - Word Frequency Counter

**Question:** Count frequency of each word in a sentence.

```java
import java.util.*;

public class WordFrequency {
    public static void main(String[] args) {
        String sentence = "java is fun and java is powerful";
        String[] words = sentence.split(" ");

        Map<String, Integer> wordCount = new HashMap<>();

        for (String word : words) {
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }

        for (Map.Entry<String, Integer> entry : wordCount.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

---

### 3. Sorting with Comparable

**Question:** Sort list of objects using natural ordering.

```java
import java.util.*;

class Student implements Comparable<Student> {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int compareTo(Student s) {
        return this.name.compareTo(s.name);
    }

    public String toString() {
        return id + "-" + name;
    }
}

public class ComparableExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(2, "Rahul"));
        students.add(new Student(1, "Amit"));

        Collections.sort(students);
        System.out.println(students);
    }
}
```

---

### 4. Sorting with Comparator

**Question:** Sort using custom criteria (e.g., by salary).

```java
import java.util.*;

class Employee {
    String name;
    double salary;

    Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public String toString() {
        return name + "-" + salary;
    }
}

public class ComparatorExample {
    public static void main(String[] args) {
        List<Employee> employees = new ArrayList<>();
        employees.add(new Employee("John", 50000));
        employees.add(new Employee("Alice", 70000));

        employees.sort((e1, e2) -> Double.compare(e1.salary, e2.salary));
        System.out.println(employees);
    }
}
```

---

### 5. Remove Duplicates from List

**Question:** Remove duplicates while preserving order.

```java
import java.util.*;

public class RemoveDuplicates {
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(1, 2, 2, 3, 4, 4, 5);
        
        // Using LinkedHashSet to preserve order
        Set<Integer> set = new LinkedHashSet<>(list);
        List<Integer> result = new ArrayList<>(set);
        
        System.out.println(result); // [1, 2, 3, 4, 5]
    }
}
```

---

## File Handling & I/O

### 1. Read File Line by Line

**Question:** Read text file and count total lines.

```java
import java.io.*;

public class ReadFile {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
            String line;
            int count = 0;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
                count++;
            }
            System.out.println("Total lines: " + count);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

### 2. Write to File

**Question:** Write multiple lines to a text file.

```java
import java.io.*;

public class WriteFile {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
            bw.write("Line 1");
            bw.newLine();
            bw.write("Line 2");
            System.out.println("File written successfully!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

### 3. Object Serialization

**Question:** Serialize and deserialize an object.

```java
import java.io.*;

class Student implements Serializable {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public String toString() {
        return id + "-" + name;
    }
}

public class SerializationDemo {
    public static void main(String[] args) {
        Student s = new Student(1, "John");

        // Serialize
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("student.ser"))) {
            oos.writeObject(s);
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialize
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("student.ser"))) {
            Student s2 = (Student) ois.readObject();
            System.out.println(s2);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

---

## String Manipulation

### 1. Reverse a String

```java
public class ReverseString {
    public static String reverse(String str) {
        return new StringBuilder(str).reverse().toString();
    }
    
    // Manual approach
    public static String reverseManual(String str) {
        char[] arr = str.toCharArray();
        int left = 0, right = arr.length - 1;
        while (left < right) {
            char temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
        return new String(arr);
    }
}
```

---

### 2. Check Palindrome

```java
public class PalindromeCheck {
    public static boolean isPalindrome(String str) {
        String reversed = new StringBuilder(str).reverse().toString();
        return str.equals(reversed);
    }
}
```

---

### 3. Count Vowels and Consonants

```java
public class VowelConsonantCount {
    public static void count(String str) {
        int vowels = 0, consonants = 0;
        str = str.toLowerCase();
        
        for (char ch : str.toCharArray()) {
            if (Character.isLetter(ch)) {
                if ("aeiou".indexOf(ch) != -1) {
                    vowels++;
                } else {
                    consonants++;
                }
            }
        }
        
        System.out.println("Vowels: " + vowels + ", Consonants: " + consonants);
    }
}
```

---

### 4. Find First Non-Repeated Character

```java
import java.util.*;

public class FirstNonRepeated {
    public static char findFirst(String str) {
        Map<Character, Integer> map = new LinkedHashMap<>();
        
        for (char ch : str.toCharArray()) {
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }
        
        for (Map.Entry<Character, Integer> entry : map.entrySet()) {
            if (entry.getValue() == 1) {
                return entry.getKey();
            }
        }
        return '\0';
    }
}
```

---

### 5. Anagram Check

```java
import java.util.Arrays;

public class AnagramCheck {
    public static boolean isAnagram(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        
        char[] arr1 = s1.toCharArray();
        char[] arr2 = s2.toCharArray();
        
        Arrays.sort(arr1);
        Arrays.sort(arr2);
        
        return Arrays.equals(arr1, arr2);
    }
}
```

---

## Important Concepts

### 1. Immutable Class

```java
public final class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
}
```

---

### 2. Singleton Pattern

```java
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

---

### 3. equals() and hashCode()

```java
import java.util.Objects;

class Student {
    private int id;
    private String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Student)) return false;
        Student student = (Student) o;
        return id == student.id && name.equals(student.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }
}
```

---

### 4. Functional Interface & Lambda

```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

public class LambdaExample {
    public static void main(String[] args) {
        Calculator add = (a, b) -> a + b;
        Calculator multiply = (a, b) -> a * b;
        
        System.out.println(add.calculate(5, 3));      // 8
        System.out.println(multiply.calculate(5, 3)); // 15
    }
}
```

---

## Common Interview Patterns

| Problem Type | Key Concepts |
|--------------|--------------|
| Find duplicates in array | HashSet, HashMap |
| Sort objects | Comparable, Comparator |
| Thread safety | synchronized, volatile |
| File operations | BufferedReader, BufferedWriter |
| String manipulation | StringBuilder, char array |
| Exception handling | try-catch-finally, custom exceptions |
| Design patterns | Singleton, Factory |

---

## Tips for Coding Round

1. **Always handle exceptions** - Use try-catch for file/network operations
2. **Use appropriate collections** - ArrayList for order, HashSet for uniqueness, HashMap for key-value
3. **Optimize string operations** - Use StringBuilder for concatenation
4. **Write clean code** - Proper naming, indentation, comments
5. **Test edge cases** - null values, empty arrays, boundary conditions
6. **Know time complexity** - Be ready to explain your solution's efficiency
