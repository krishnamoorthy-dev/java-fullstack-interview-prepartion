# Hibernate Interview Concepts – Detailed README

## 1. What is ORM?

Object Relational Mapping (ORM) is a programming technique used to map Java objects to relational database tables. ORM eliminates the need for developers to write repetitive SQL by allowing them to interact with the database using objects.

### Key Benefits

* Reduces boilerplate SQL
* Makes code database-agnostic
* Improves productivity and maintainability
* Supports caching, lazy loading, transactions, and more

Hibernate is one of the most widely used ORM frameworks in the Java world.

---

## 2. Hibernate Life Cycle

Hibernate objects go through the following states:

### **1. Transient State**

* The object is created using the `new` keyword
* Not associated with any Hibernate session
* Not persisted in the database

### **2. Persistent State**

* Object is associated with a Hibernate `Session`
* Any changes made are tracked and synchronized with DB via automatic dirty checking

### **3. Detached State**

* Object was persistent but the session is closed or the object was evicted
* Changes made now are not automatically saved unless reattached (e.g., `update()` or `merge()`)

---

## 3. Hibernate Architecture

Hibernate architecture consists of:

### **1. Configuration**

Loads Hibernate configuration (XML/properties/annotations) and builds the SessionFactory.

### **2. SessionFactory**

* Heavyweight object, created once per application
* Thread-safe and immutable
* Creates Session objects

### **3. Session**

* A lightweight, non-thread-safe object
* Represents one unit of work

### **4. Transaction**

* Ensures ACID properties
* Wraps a set of operations into a single logical unit

### **5. Query / Criteria API**

* Used to perform CRUD and retrieval operations

### **6. JDBC / Database Layer**

* Hibernate internally uses JDBC to communicate with the database

---

## 4. Level 1 Cache vs Level 2 Cache

### **Level 1 Cache (L1 Cache)**

* Default cache
* Exists at Session level
* Cannot be disabled
* Stores objects loaded within the current session

### **Level 2 Cache (L2 Cache)**

* Optional cache
* Exists at SessionFactory level
* Shared across sessions
* Providers: Ehcache, Hazelcast, Infinispan
* Used for improving read performance

---

## 5. Hibernate Annotations

### **@Entity**

Marks a class as a persistent POJO.

### **@Table(name = "table_name")**

Defines the database table name for the entity.

### **@OneToOne**

Defines a one-to-one relationship between two entities.

### **@ManyToOne**

Many child records mapped to one parent record.

### **@OneToMany**

One parent has multiple child records.

### **@ManyToMany**

Many-to-many relationship using a join table.

### **@Transient**

Marks a field that should not be persisted to the database.

---

## 6. Table Relation Annotations

### **@JoinColumn(name = "column_name")**

Defines the foreign key column.

### **@JoinTable**

Used for many-to-many or custom join tables.

### **@MappedBy**

Indicates the owning side of the relationship.

---

## 7. Hibernate CRUD Methods

### **save()**

* Inserts a new record
* Returns generated identifier
* Can create duplicates if called for existing entity

### **persist()**

* Similar to save()
* Doesn’t return ID
* Follows JPA specification

### **update()**

* Updates a detached entity
* Throws exception if entity already exists in session

### **merge()**

* Safely merges detached entity state into persistent context
* Does not throw if object exists in session

### **saveOrUpdate()**

* Inserts if entity has no ID
* Updates if entity has ID

---

## 8. get() vs load()

### **get()**

* Immediately hits database
* Returns null if record not found
* Eager fetching

### **load()**

* Returns a proxy object
* Sends query only when needed
* Throws `ObjectNotFoundException` if record doesn’t exist

---

## 9. Pessimistic vs Optimistic Locking

### **Optimistic Locking**

* Uses versioning (e.g., `@Version`)
* Assumes multiple transactions rarely conflict
* Fast and preferred for high-concurrency systems

### **Pessimistic Locking**

* Locks the row during reading/updating
* Prevents other transactions from modifying the row
* Slower but safe for high-conflict scenarios

---

## 10. SessionFactory vs Session

### **SessionFactory**

* Heavyweight
* Thread-safe
* Usually one instance per application
* Creates sessions

### **Session**

* Lightweight and short-lived
* Not thread-safe
* Represents a unit of work

---

## 11. getCurrentSession() vs openSession()

### **getCurrentSession()**

* Returns session bound to current context (ex: thread)
* Automatically closed after transaction

### **openSession()**

* Creates a new session every time
* Must be closed manually

---

## 12. SQL Injection

SQL Injection is a security attack where malicious users inject SQL code into queries.

### Prevention in Hibernate

* Use parameterized queries (`:name`)
* Avoid string concatenation
* Use Criteria API or JPA Queries

---

## 13. Automatic Dirty Checking in Hibernate

Hibernate tracks changes to persistent objects.

### How it works

* When an entity is in persistent state
* Hibernate compares the current state with the snapshot
* If any field is modified, Hibernate automatically updates the database during flush

### Benefits

* Reduces need for manual `update()` calls
* Improves developer productivity

---

## 14. Hibernate save(), persist(), update(), merge(), saveOrUpdate() – Detailed with Examples

### 1. **save()**

* Inserts a new row in the database
* Returns the generated identifier (Serializable)
* Works in Hibernate-specific API (not JPA)
* Executes INSERT immediately or during flush

#### Example

```java
Student s = new Student();
s.setName("John");
Serializable id = session.save(s); // returns ID
```

---

### 2. **persist()**

* Similar to save()
* Does NOT return ID
* JPA-compliant
* Ensures entity becomes persistent but insert may occur at flush time

#### Example

```java
Student s = new Student();
s.setName("John");
session.persist(s);  // no return value
```

---

### 3. **update()**

* Reattaches a detached entity
* Throws exception if the entity with same identifier already exists in session

#### Example

```java
Student s = session.get(Student.class, 1);
session.evict(s);  // make detached
s.setName("Updated");
session.update(s);  // entity becomes persistent
```

---

### 4. **merge()**

* Safely merges detached entity state
* NO exception if persistent entity already exists in session
* Returns a new managed copy of the entity

#### Example

```java
Student detached = new Student(1, "John");
Student persistent = (Student) session.merge(detached);
```

---

### 5. **saveOrUpdate()**

* If entity has no ID → INSERT
* If entity has ID → UPDATE

#### Example

```java
Student s = new Student();
s.setId(1);
s.setName("John Updated");
session.saveOrUpdate(s);
```

---

## 15. Hibernate Relationship Annotations – With Examples

## @Entity and @Table

```java
@Entity
@Table(name = "students")
public class Student {
    @Id
    private int id;
    private String name;
}
```

---

## @OneToOne Example

```java
@Entity
public class User {
    @Id
    private int id;

    @OneToOne
    @JoinColumn(name = "profile_id")
    private Profile profile;
}
```

---

## @ManyToOne Example

```java
@Entity
public class Employee {
    @Id
    private int id;

    @ManyToOne
    @JoinColumn(name = "dept_id")
    private Department department;
}
```

---

## @OneToMany Example

```java
@Entity
public class Department {
    @Id
    private int id;

    @OneToMany(mappedBy = "department")
    private List<Employee> employees;
}
```

---

## @ManyToMany Example

```java
@Entity
public class Student {
    @Id
    private int id;

    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private List<Course> courses;
}
```

---

## @Transient Example

```java
@Transient
private int tempValue;   // will not be saved in DB
```

---

## 16. Table Relation Annotations – Detailed

### @JoinColumn

Defines foreign key column.

```java
@JoinColumn(name = "dept_id")
```

### @JoinTable

Used in Many-to-Many or custom join table mapping.

```java
@JoinTable(
    name = "student_course",
    joinColumns = @JoinColumn(name = "student_id"),
    inverseJoinColumns = @JoinColumn(name = "course_id")
)
```

### @MappedBy

Defines the inverse (non-owning) side of relation.

```java
@OneToMany(mappedBy = "department")
```

---

**End of Document**
