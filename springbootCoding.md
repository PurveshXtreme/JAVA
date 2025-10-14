# Student Management REST API — Full Code (using your provided code)

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
