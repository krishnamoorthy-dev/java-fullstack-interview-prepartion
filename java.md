# ☕ Java Interview Preparation Guide

A concise and easy-to-understand guide covering core Java concepts for interviews.

This guide covers:

* Core Java fundamentals
* OOP & design principles
* Collections & multithreading
* Modern Java features

---

## 📌 Java Basics

### 🔹 JVM, JRE, JDK

| Component                          | Description                                                 |
| ---------------------------------- | ----------------------------------------------------------- |
| **JVM (Java Virtual Machine)**     | Executes Java bytecode and provides platform independence   |
| **JRE (Java Runtime Environment)** | Contains JVM + libraries required to run Java applications  |
| **JDK (Java Development Kit)**     | Contains JRE + development tools (compiler, debugger, etc.) |

---

## 📦 Class Loaders

Java uses class loaders to load classes into memory:

* **Bootstrap Class Loader**

  * Loads core Java classes (`java.lang`, `java.util`)
* **Platform Class Loader**

  * Loads Java SE APIs (`java.sql`, etc.)
* **Application Class Loader**

  * Loads classes from application classpath

---

## 🧱 OOP Concepts

| Concept           | Description                                               |
| ----------------- | --------------------------------------------------------- |
| **Abstraction**   | Hides implementation details and shows only functionality |
| **Encapsulation** | Wrapping data and methods into a single unit (class)      |
| **Inheritance**   | One class acquires properties of another                  |
| **Polymorphism**  | Same method behaves differently (overloading/overriding)  |

---

## 🔁 equals() and hashCode()

* If two objects are equal using `equals()`, they **must have the same hashCode()**
* Used in collections like `HashMap`, `HashSet`
* Always override both together

---

## ⚙️ Static vs Instance Block

| Type | Execution Time | Example |
|-------|----------------|----------|
| **Static Block** | Runs once when class loads. | `static { System.out.println("Class loaded"); }` |
| **Instance Block** | Runs each time an object is created. | `{ System.out.println("Object created"); }` |

---

## 🧩 SOLID Principles

* **S - Single Responsibility Principle**

  * A class should have only one reason to change

* **O - Open/Closed Principle**

  * Open for extension, closed for modification

* **L - Liskov Substitution Principle**

  * Subclass should replace parent without issues

* **I - Interface Segregation Principle**

  * Prefer smaller, specific interfaces

* **D - Dependency Inversion Principle**

  * Depend on abstractions, not concrete classes

---

## 🆚 Interface vs Abstract Class

| Feature     | Interface                                       | Abstract Class             |
| ----------- | ----------------------------------------------- | -------------------------- |
| Methods     | Only abstract (Java 8+: default/static allowed) | Abstract + concrete        |
| Variables   | Public static final                             | Instance variables allowed |
| Inheritance | Multiple                                        | Single                     |

---

## ♻️ Garbage Collection

An object becomes **eligible for garbage collection (GC)** when no live reference exists.

### ✅ Ways to make objects eligible:
1. **Nullifying reference**
   ```java
   obj = null;
   ```
2. **Reassigning reference**
   ```java
   Demo d1 = new Demo();
   d1 = new Demo(); // old object eligible for GC
   ```
3. **Anonymous object**
   ```java
   new Demo(); // No reference, eligible after use
   ```
4. **Objects inside methods** (after method ends)
   ```java
   void create() {
       Demo d = new Demo();
   } // eligible after method ends
   ```

### 🔹 Manual GC Trigger

```java
System.gc(); // Requests JVM to run garbage collector
```

> Note: JVM decides when to run GC

---

## 🔍 Final vs Finally vs Finalize

| Keyword        | Usage                                  |
| -------------- | -------------------------------------- |
| **final**      | Constant, prevent inheritance          |
| **finally**    | Always executes in try-catch           |
| **finalize()** | Called by GC before object destruction |

---

## 📚 Collections Framework

### 🔹 List

* `ArrayList` → Fast access
* `LinkedList` → Fast insert/delete
* `Vector` → Thread-safe
* `Stack` → LIFO

### 🔹 Set

* `HashSet` → No order
* `TreeSet` → Sorted

### 🔹 Queue

* `PriorityQueue` → Priority-based
* `ArrayDeque` → Faster than stack/queue

---

## 📚 ArrayList vs LinkedList
| Feature | ArrayList | LinkedList |
|----------|------------|-------------|
| Storage | Dynamic array | Doubly linked list |
| Access Speed | Fast (O(1)) | Slow (O(n)) |
| Insert/Delete | Slow | Fast |
| Memory Usage | Compact | More overhead |

---

## 🗝️ Hashtable
- Thread-safe, synchronized.
- Doesn’t allow null keys/values.
- Slower than HashMap.

---

## 🗂️ HashMap vs HashSet
| Feature | HashMap | HashSet |
|----------|----------|----------|
| Structure | Key-Value pair | Unique elements only |
| Allows Null | One null key | One null element |
| Internally Uses | Buckets | HashMap internally |

---

## 💎 Diamond Problem

* Occurs in multiple inheritance
* Java avoids it using **interfaces with default methods**

---

## 🗺️ HashMap Internal Working

* Uses **array + linked list / tree**
* Steps:

  1. Calculate hash
  2. Find bucket index
  3. Handle collision:

     * Linked List (Java 7)
     * Balanced Tree (Java 8+)

---

## ⚠️ Exception vs Error

| Type | Checked by Compiler | Example |
|-------|----------------------|----------|
| **Checked** | Yes | IOException, SQLException |
| **Unchecked** | No | NullPointerException, ArithmeticException |

---

## 🛡️ Exception Handling

* **Checked Exception** → Compile-time (IOException)
* **Unchecked Exception** → Runtime (NullPointerException)

---

## 🔄 Fail-Fast vs Fail-Safe

| Type          | Behavior                                       |Example |
| ------------- | ---------------------------------------------- |--------|
| **Fail-Fast** | Throws exception if modified                   |ArrayList, HashMap |
| **Fail-Safe** | Works on copy (e.g., CopyOnWriteArrayList)     |CopyOnWriteArrayList, ConcurrentHashMap |

---

## 🔀 Comparator vs Comparable

| Feature | Comparable | Comparator |
|----------|-------------|-------------|
| Package | java.lang | java.util |
| Method | compareTo() | compare() |
| Sorting Type | Natural order | Custom order |
| Example | `class Emp implements Comparable<Emp>` | `Comparator<Emp> byName` |

---

## 🧵 Thread

### 🔹 Thread Life Cycle

* New → Runnable → Running → Waiting → Terminated

### 🔹 Executor Service

* Manages thread pool efficiently

### 🔹 CompletableFuture

* Asynchronous programming

---

### 🔹 Thread Important Methods

```java
join()   // Waits for thread to finish
sleep()  // Pauses execution
yield()  // Gives chance to other threads
```

---

## ⛔ Stopping Main Thread

* Using:

  * `System.exit()`
  * Daemon threads
  * Exception

---

## 🔒 Deadlock

* Situation where two threads wait for each other forever

---

## 🧠 Design Patterns

### 🔹 Creational

* Singleton, Factory, Builder

### 🔹 Structural

* Adapter, Decorator

### 🔹 Behavioral

* Observer, Strategy

---

## 🚀 Java Features (LTS Versions)

### 🔹 JDK 8

* Stream API
* Lambda Expressions
* Optional
* Functional Interfaces
* Default methods in interface
* Date & Time API

---

### 🔹 JDK 11

* New String methods:

  * `isBlank()`
  * `lines()`
  * `strip()`

---

### 🔹 JDK 17

* Sealed Classes
* Records
* Text Blocks
* Pattern Matching (`instanceof`)
* Enhanced Switch

---
