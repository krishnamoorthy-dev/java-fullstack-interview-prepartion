# 🌱 Spring & Spring Boot Interview Answers

---

## 📌 1. Spring Boot Architecture
Spring Boot architecture includes:

- **Spring Core** – IoC, DI  
- **Auto-Configuration** – Configures beans automatically  
- **Spring Boot Starters** – Predefined dependency bundles  
- **Embedded Servers** – Tomcat, Jetty, Undertow  
- **Spring Actuator** – Health checks, metrics  
- **Logging** – Logback, JUL  
- **Spring Boot CLI / DevTools** – Faster development workflow  

Focus:
- Convention over configuration  
- Minimal XML  
- Production-ready  

---

## 📌 2. Spring MVC Architecture
Spring MVC follows **Model–View–Controller**:

**Flow:**
1. Request → DispatcherServlet  
2. DispatcherServlet → HandlerMapping  
3. HandlerMapping → Controller  
4. Controller → Service → Repository  
5. Controller returns Model + View  
6. ViewResolver selects view  
7. Response returned to client  

Components:
- DispatcherServlet  
- Controllers  
- Models  
- Views  
- ViewResolver  
- HandlerMapping  

---

## 📌 3. Spring Scopes

| Scope | Description |
|-------|-------------|
| **singleton** | One instance per container |
| **prototype** | New instance every time requested |
| **request** | One instance per HTTP request |
| **session** | One instance per HTTP session |
| **application** | One instance per ServletContext |
| **websocket** | One instance per WebSocket session |

---

## 📌 4. Spring Stereotype Annotations
- **@Component** – Generic Spring bean  
- **@Service** – Business logic  
- **@Repository** – Data access layer, exception translation  
- **@Controller** – Web MVC controller  
- **@RestController** – REST API controller  

---

## 📌 5. Explain @SpringBootApplication
`@SpringBootApplication` =  
- **@Configuration**  
- **@EnableAutoConfiguration**  
- **@ComponentScan**  

It marks the starting point of a Spring Boot application.

---

## 📌 6. @Controller vs @RestController

| @Controller | @RestController |
|------------|-----------------|
| Returns HTML/JSP views | Returns JSON/XML |
| Uses ViewResolver | Sends response body directly |
| Requires @ResponseBody for JSON | Includes it automatically |

---

## 📌 7. @RequestMapping vs @GetMapping

| @RequestMapping | @GetMapping |
|----------------|-------------|
| Generic, supports all HTTP methods | Short-hand for GET |
| Verbose when mapping GET | More readable |

---

## 📌 8. @PutMapping vs @PatchMapping

| Annotation | Meaning |
|-----------|---------|
| **@PutMapping** | Full update (replace entire entity) |
| **@PatchMapping** | Partial update (modify only specific fields) |

---

## 📌 9. @RequestParam vs @PathVariable vs @RequestBody

| Annotation | Usage |
|-----------|--------|
| **@RequestParam** | Query parameters (`?id=1`) |
| **@PathVariable** | Dynamic URI values (`/user/1`) |
| **@RequestBody** | Maps JSON body to a POJO |

---

## 📌 10. How will you handle exceptions globally in Spring Boot?

Use **@ControllerAdvice + @ExceptionHandler**:

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<?> handleAll(Exception ex) {
        return ResponseEntity.badRequest().body(ex.getMessage());
    }
}
````

---

## 📌 11. CRUD Repository vs JPA Repository

| CrudRepository               | JpaRepository              |
| ---------------------------- | -------------------------- |
| Basic CRUD only              | CRUD + JPA features        |
| save(), findById(), delete() | Pagination, Sorting, Batch |
| Limited                      | Richer API                 |

JpaRepository extends CrudRepository.

---

## 📌 12. ACID Properties

* **Atomicity** – All or none
* **Consistency** – Ensures valid data
* **Isolation** – Independent transactions
* **Durability** – Persistent after commit

---

## 📌 13. How to roll back changes for specific exception?

```java
@Transactional(rollbackFor = CustomException.class)
public void execute() {
    // logic
}
```

---

## 📌 14. Transaction Isolation & Propagation

### **Isolation Levels**

* READ_UNCOMMITTED
* READ_COMMITTED
* REPEATABLE_READ
* SERIALIZABLE

### **Propagation Levels**

* REQUIRED
* REQUIRES_NEW
* SUPPORTS
* NOT_SUPPORTED
* NEVER
* MANDATORY
* NESTED

---

## 📌 15. What is Eager vs Lazy Loading?

| Type              | Description                               |
| ----------------- | ----------------------------------------- |
| **Eager Loading** | Loads related entities immediately        |
| **Lazy Loading**  | Loads related entities only when accessed |

Lazy is preferred for optimization.

---

## 📌 16. What is N+1 Problem?

Occurs when:

* 1 query fetches parent data
* N additional queries fetch each child data

Example:

```
SELECT * FROM users;
SELECT * FROM orders WHERE user_id = 1;
SELECT * FROM orders WHERE user_id = 2;
...
```

**Fixes:**

* JOIN FETCH
* @EntityGraph
* Batch fetching

---

## 📌 17. What is HandlerInterceptor in Spring Boot?

Interceptor to pre/post process requests.

Methods:

* `preHandle()` – before controller
* `postHandle()` – after controller
* `afterCompletion()` – after request complete

Used for:

* Logging
* Authentication
* Modifying request/response

---

## 📌 18. What is Filter in Spring Boot?

A Servlet-level filter executes **before and after** request processing.

Used for:

* Logging
* Security
* CORS
* Request validation

Executed **before DispatcherServlet**.

---

## 📌 19. Caching in Spring Boot

Enable caching:

```java
@EnableCaching
@SpringBootApplication
public class App {}
```

Add caching:

```java
@Cacheable("users")
public User getUser(int id) { ... }

@CachePut("users")
public User updateUser(User u) { ... }

@CacheEvict("users")
public void deleteUser(int id) { }
```

Supported cache providers:

* ConcurrentMap
* Redis
* Caffeine
* EhCache

---
