# Table of Contents

- [Go to Student Management REST API](#student-management-rest-api)
- [Go to To-Do Tracker with Status](#to-do-tracker-with-status)
- [Banking Transaction API](#banking-transaction-api)
- [Jump to Library Management (Book + Author)](#4-library-management-book--author)



---
---


# Student Management REST API 

**Problem:**  
Create a Spring Boot app to manage students.  
Each student has: `id`, `name`, `email`, `department`.  

**Endpoints:**  
- `POST /students` → Add a new student.  
- `GET /students` → Get all students.  
- `GET /students/{id}` → Get a student by ID.  
- `PUT /students/{id}` → Update student details.  
- `DELETE /students/{id}` → Delete a student.  

**Tests/Concepts Tested:**  
- Handle “student not found” gracefully.  
- Validate email format and non-empty name.  
- Concepts: CRUD, REST design, `@Valid`, exception handling, Spring Data JPA.  

---

# 📦 Dependencies Used

- **Spring Web**  
- **Lombok**  
- **Spring Data JPA**  
- **MySQL Driver**  
- **Validation**


---

## `src/main/resources/application.properties`

```properties
spring.application.name=demo
# MySQL Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/interviewprep
spring.datasource.username=root
spring.datasource.password=dsadsa
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect

# JPA Config
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

---

## `src/main/java/com/interview/demo/model/User.java`

```java
// @Data (Lombok) generates getters, setters, toString, equals, and hashCode methods.
// @NoArgsConstructor (Lombok) generates a no-argument constructor.
// @AllArgsConstructor (Lombok) generates an all-arguments constructor.
// @Entity marks the class as a JPA entity mapped to a database table.
@Data
@NoArgsConstructor
@AllArgsConstructor
@Entity
public class User {

    // @Id marks the primary key field of the entity.
    // @GeneratedValue(strategy = GenerationType.AUTO) tells JPA to auto-generate the id value.
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;

    // @NotBlank ensures the name is not null/empty/blank when validated (Jakarta Validation).
    @NotBlank(message = "Name cannot be Empty!")
    private String name;

    // @NotBlank ensures email is not empty; @Email validates proper email format.
    @NotBlank(message = "Email cannot be Empty!")
    @Email(message = "Incorrect email format")
    private String email;

    // department is optional (no validation).
    private String department;
}
```

---

## `src/main/java/com/interview/demo/repo/UserRepo.java`

```java
// @Repository indicates a Spring Data repository (optional when extending JpaRepository).
// Extending JpaRepository<User, Long> provides CRUD methods like save, findById, findAll, delete.
@Repository
public interface UserRepo extends JpaRepository<User , Long> {
}
```

---

## `src/main/java/com/interview/demo/service/UserService.java`

```java
// @Service marks this class as a Spring service component (business logic layer).
@Service
public class UserService {

    // @Autowired injects the UserRepo bean so we can use JPA methods.
    @Autowired
    private UserRepo userRepo;

    // Create a new user and persist it to the database.
    public User createUser(User user) {
        return userRepo.save(user);
    }

    // Retrieve and return all users from the database.
    public List<User> getAllUsers() {
        return userRepo.findAll();
    }

    // Retrieve a user by id; throw RuntimeException if not found.
    public User getUserById(long id) {
        return userRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("User not found"));
    }

    // Update existing user's fields and save; throw RuntimeException if user not found.
    public User updateUser(long id, User userDetails) {
        User oldUser = userRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("User not found"));
        oldUser.setName(userDetails.getName());
        oldUser.setEmail(userDetails.getEmail());
        oldUser.setDepartment(userDetails.getDepartment());
        return userRepo.save(oldUser);
    }

    // Delete a user by id; throw RuntimeException if user not found.
    public void deleteUser(long id) {
        User user = userRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("User not found"));
        userRepo.delete(user);
    }
}
```

---

## `src/main/java/com/interview/demo/controller/UserController.java`

```java
// @RestController combines @Controller and @ResponseBody: controller whose methods return JSON by default.
// @RequestMapping("/api/users") sets the base path for all endpoints in this controller.
@RestController
@RequestMapping("/api/users")
public class UserController {

    // @Autowired injects the UserService bean to delegate business logic.
    @Autowired
    private UserService userService;

    // POST /api/users/register
    // Creates a new user (validates request body because @Valid is present).
    @PostMapping("/register")
    public User createUser(@Valid @RequestBody User user) {
        return userService.createUser(user);
    }

    // GET /api/users/
    // Returns a list of all users.
    @GetMapping("/")
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }

    // GET /api/users/{id}
    // Returns a single user by path variable id.
    @GetMapping("/{id}")
    public User getUserById(@PathVariable long id) {
        return userService.getUserById(id);
    }

    // PUT /api/users/update/{id}
    // Updates the user with the given id using provided user fields.
    @PutMapping("/update/{id}")
    public User updateUser(@PathVariable long id, @RequestBody User user) {
        return userService.updateUser(id, user);
    }

    // DELETE /api/users/{id}
    // Deletes the user with the given id.
    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable long id) {
        userService.deleteUser(id);
    }
}
```

---

### Notes (minimal, only to help run)
- Ensure your `application.properties` credentials and DB exist.
- Use `mvn spring-boot:run` to start the app.
- Test endpoints at `http://localhost:8080/api/users` (as you requested earlier).

---
---

# To-Do Tracker with Status 

**Problem:**  
Build a REST API for To-Do tasks.  
Each task has: `id`, `title`, `description`, `status` (PENDING/DONE).  

**Endpoints:**  
- `POST /tasks` → Add new task.  
- `PUT /tasks/{id}/status` → Update task status.  
- `GET /tasks?status=PENDING` → Filter by status.  

**Tests/Concepts Tested:**  
- Return 400 for invalid status.  
- Return 404 for missing task.  
- Concepts: Request params, filtering, REST best practices.  

---

## Todo.java (Model)

```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Todo {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private int id; // Auto-generated task ID

    @NotBlank(message = "Title cannot be blank")
    private String title; // Task title

    private String description; // Task description

    @Enumerated(EnumType.STRING)
    private Status status = Status.PENDING; // Default status is PENDING

    // Enum defined inside the class for task status
    public enum Status {
        PENDING, DONE
    }
}
```

---

## TodoRepo.java (Repository)

```java
@Repository
public interface TodoRepo extends JpaRepository<Todo, Integer> {

    // Custom query method to filter tasks by status
    List<Todo> findByStatus(Todo.Status status);
}
```

---

## TodoService.java (Service Layer)

```java
@Service
public class TodoService {

    @Autowired
    private TodoRepo todoRepo;

    // Add a new task
    public Todo addTodo(Todo todo) {
        return todoRepo.save(todo);
    }

    // Toggle the status of a task (PENDING ↔ DONE)
    public Todo toggleStatus(int id) {
        Todo todo = todoRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("Task Not Found!"));

        if (todo.getStatus() == Todo.Status.PENDING) {
            todo.setStatus(Todo.Status.DONE);
        } else {
            todo.setStatus(Todo.Status.PENDING);
        }

        return todoRepo.save(todo);
    }

    // Get all tasks
    public List<Todo> getAllTodo() {
        return todoRepo.findAll();
    }

    // Get tasks filtered by status
    public List<Todo> findByStatus(Todo.Status status) {
        return todoRepo.findByStatus(status);
    }
}
```

---

## TodoController.java (Controller Layer)

```java
@RestController
@RequestMapping("/api/todo")
public class TodoController {

    @Autowired
    private TodoService todoService;

    // POST /api/todo/ → Add a new task
    @PostMapping("/")
    public Todo addTodo(@Valid @RequestBody Todo todo) {
        return todoService.addTodo(todo);
    }

    // PUT /api/todo/{id}/status → Toggle task status
    @PutMapping("/{id}/status")
    public Todo toggleStatus(@PathVariable int id) {
        return todoService.toggleStatus(id);
    }

    // GET /api/todo → Get all tasks or filter by status
    // Example: GET /api/todo?status=PENDING
    @GetMapping
    public List<Todo> getTodos(@RequestParam(required = false) Todo.Status status) {
        if (status != null) {
            return todoService.findByStatus(status);
        }
        return todoService.getAllTodo();
    }
}
```

---

### ✅ Summary

- **POST `/api/todo/`** → Add a new task.  
- **PUT `/api/todo/{id}/status`** → Toggle the status of a task.  
- **GET `/api/todo`** → Get all tasks or filter by status with query param `?status=PENDING` or `?status=DONE`.  
- Default task status is **PENDING**.  
- Uses **Enum** for status to prevent invalid values.  
- Custom repository method `findByStatus` allows filtering efficiently.

---
---

# Banking Transaction API

**Problem:**  
Design an API for simple bank accounts.  
Each account has: `id`, `name`, `balance`.  

**Endpoints:**  
- `POST /accounts` → Create new account (balance starts at 0).  
- `PUT /accounts/{id}/deposit` → Add amount.  
- `PUT /accounts/{id}/withdraw` → Subtract amount.  

**Constraints/Concepts Tested:**  
- Prevent overdraft (balance < 0).  
- Concepts: Basic CRUD, transactional updates, exception handling.  

---

```java
// ✅ model/Account.java
package com.interview.demo.model;

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Account {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;

    @NotBlank(message = "Name cannot be null")
    private String name;

    private long balance = 0;
}
```

```java
// ✅ repo/AccountRepo.java
package com.interview.demo.repo;

@Repository
public interface AccountRepo extends JpaRepository<Account, Long> {
}
```

```java
// ✅ service/AccountService.java
package com.interview.demo.service;

@Service
public class AccountService {

    @Autowired
    private AccountRepo accountRepo;

    public Account createAccount(String name) {
        Account account = new Account();
        account.setName(name);
        return accountRepo.save(account);
    }

    public Account addAmount(long id, long amount) {
        Account account = accountRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("Account not found!"));

        account.setBalance(account.getBalance() + amount);
        return accountRepo.save(account);
    }

    public Account subAmount(long id, long amount) throws Exception {
        Account account = accountRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("Account not found!"));

        long currentBalance = account.getBalance();
        if (currentBalance < amount) {
            throw new Exception("Not enough balance");
        }

        account.setBalance(currentBalance - amount);
        return accountRepo.save(account);
    }

    public List<Account> getAllAccounts() {
        return accountRepo.findAll();
    }
}
```

```java
// ✅ controller/AccountController.java
package com.interview.demo.controller;

@RestController
@RequestMapping("/api/account")
public class AccountController {

    @Autowired
    private AccountService accountService;

    // DTO for request body containing amount
    public static class AmountRequest {
        public long amount;
    }

    @GetMapping("/")
    public List<Account> getAllAccounts() {
        return accountService.getAllAccounts();
    }

    @PostMapping("/")
    public Account createAccount(@RequestBody Account account) {
        return accountService.createAccount(account.getName());
    }

    @PutMapping("/{id}/deposit")
    public Account deposit(@PathVariable long id, @RequestBody AmountRequest request) {
        return accountService.addAmount(id, request.amount);
    }

    @PutMapping("/{id}/withdraw")
    public Account withdraw(@PathVariable long id, @RequestBody AmountRequest request) throws Exception {
        return accountService.subAmount(id, request.amount);
    }
}
```

---
---

# 4. Library Management (Book + Author)

**Problem:**  
Create a REST API with two entities: Book and Author.  
Each author can have multiple books.  

**Endpoints:**  
- Add new author.  
- Add book to author.  
- List books by author.  

**Concepts Tested:**  
- One-to-Many mapping, `@JoinColumn`, DTO mapping, JPA relationships.

---

```java
// ------------------------- Book.java -------------------------
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Book {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;

    @NotBlank(message = "Title cannot be Blank")
    private String title;

    // Many books belong to one author
    @ManyToOne
    @JoinColumn(name = "author_id")  // foreign key in book table
    private Author author;
}
```

```java
// ------------------------- Author.java -------------------------
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Author {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;

    @NotBlank(message = "Name cannot be blank")
    private String name;

    @NotBlank(message = "Email cannot be blank")
    @Email(message = "Invalid Email")
    private String email;

    // One author has many books
    @OneToMany(mappedBy = "author", cascade = CascadeType.ALL)
    private List<Book> books = new ArrayList<>();
}
```

```java
// ------------------------- AuthorRepo.java -------------------------
@Repository
public interface AuthorRepo extends JpaRepository<Author , Long> {
}
```

```java
// ------------------------- BookRepo.java -------------------------
@Repository
public interface BookRepo extends JpaRepository<Book , Long> {
     List<Book> findByAuthor(Author author);
}
```

```java
// ------------------------- AuthorService.java -------------------------
@Service
public class AuthorService {

    @Autowired
    private AuthorRepo authorRepo;

    // Add new author
    public Author addNewAuthor(Author author){
        return authorRepo.save(author);
    }

    // Get all authors
    public List<Author> getAllAuthors(){
        return authorRepo.findAll();
    }

    // Get author by id
    public Author getAuthorById(long id){
        return authorRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("Author does not Exists"));
    }
}
```

```java
// ------------------------- BookService.java -------------------------
@Service
public class BookService {

    @Autowired
    private BookRepo bookRepo;

    @Autowired
    private AuthorService authorService;

    // Add new book for a specific author
    public Book addNewBook(Book book , long authorId){
        Author author = authorService.getAuthorById(authorId);
        Book newBook = new Book();
        newBook.setAuthor(author);
        newBook.setTitle(book.getTitle());
        return bookRepo.save(newBook);
    }

    // Get all books
    public List<Book> getAllBooks(){
        return bookRepo.findAll();
    }

    // Get books by author
    public List<Book> getBookByAuthor(long authorId){
        Author author = authorService.getAuthorById(authorId);
        return bookRepo.findByAuthor(author);
    }
}
```

```java
// ------------------------- LibraryController.java -------------------------
@RestController
@RequestMapping("/api/lib")
public class LibraryController {

    @Autowired
    private AuthorService authorService;

    @Autowired
    private BookService bookService;

    // Add a new author
    @PostMapping("/author")
    public Author addAuthor(@Valid @RequestBody Author author){
        return authorService.addNewAuthor(author);
    }

    // Add a new book under a specific author
    @PostMapping("/author/{id}/book")
    public Book addBook(@Valid @RequestBody Book book , @PathVariable long id){
        return bookService.addNewBook(book , id);
    }

    // Get all authors
    @GetMapping("/author")
    public List<Author> getAllAuthors(){
        return authorService.getAllAuthors();
    }

    // Get all books or filter by authorId
    @GetMapping("/book")
    public List<Book> getAllBooks(@RequestParam(required = false) Long authorId){
        if(authorId != null){
            return bookService.getBookByAuthor(authorId);
        }
        return bookService.getAllBooks();
    }
}
```

---
---
