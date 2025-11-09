# Java Core Concepts - Interview Notes

A detailed **README.md** format guide for Java interview preparation.

---

## 🧩 1. SOLID Principles
| Principle | Description | Example |
|------------|-------------|----------|
| **S**ingle Responsibility | One class should have only one reason to change. | `UserService` manages users only, not emails. |
| **O**pen/Closed | Open for extension, closed for modification. | Add new logic by subclassing, not editing the existing code. |
| **L**iskov Substitution | Subclasses should be replaceable for their base classes. | `Square` can replace `Rectangle`. |
| **I**nterface Segregation | Prefer smaller, specific interfaces. | `Printer` and `Scanner` instead of one big `Machine` interface. |
| **D**ependency Inversion | Depend on abstractions, not concrete classes. | `Repository` interface instead of direct DB calls. |

---

## ⚙️ 2. Print Before `main()`
You can print before the main method using a **static block**:
```java
class Demo {
    static {
        System.out.println("Before main method");
    }
    public static void main(String[] args) {
        System.out.println("Inside main");
    }
}
```
Output:
```
Before main method
Inside main
```

---

## 🔄 3. Static vs Instance Block
| Type | Execution Time | Example |
|-------|----------------|----------|
| **Static Block** | Runs once when class loads. | `static { System.out.println("Class loaded"); }` |
| **Instance Block** | Runs each time an object is created. | `{ System.out.println("Object created"); }` |

---

## ♻️ 4. Garbage Collection Eligibility
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

---

## 🧹 5. Manual GC Trigger
```java
System.gc(); // Requests JVM to run garbage collector
```
*(Not guaranteed immediately)*

---

## 🔒 6. Final vs Finally vs Finalize
| Keyword | Purpose | Example |
|----------|----------|----------|
| **final** | Constant or prevent inheritance/override | `final int x = 10;` |
| **finally** | Executes after try-catch, always runs | Used to close resources |
| **finalize()** | Called before GC deletes object *(deprecated)* | `protected void finalize() {}` |

---

## ⚠️ 7. Exception vs Error
| Type | Meaning | Example |
|-------|----------|----------|
| **Exception** | Recoverable issues | FileNotFoundException |
| **Error** | JVM-level, unrecoverable | OutOfMemoryError |

---

## 🧾 8. Checked vs Unchecked Exceptions
| Type | Checked by Compiler | Example |
|-------|----------------------|----------|
| **Checked** | Yes | IOException, SQLException |
| **Unchecked** | No | NullPointerException, ArithmeticException |

---

## 📘 9. Try-With-Resource
Automatically closes resources after use:
```java
try (FileReader fr = new FileReader("data.txt")) {
    System.out.println((char) fr.read());
} catch (IOException e) {
    e.printStackTrace();
}
```

---

## 🚫 10. throw vs throws
| Keyword | Meaning | Example |
|----------|----------|----------|
| **throw** | Actually throw exception | `throw new IOException();` |
| **throws** | Declares exception in method signature | `void read() throws IOException {}` |

---

## 📚 11. ArrayList vs LinkedList
| Feature | ArrayList | LinkedList |
|----------|------------|-------------|
| Storage | Dynamic array | Doubly linked list |
| Access Speed | Fast (O(1)) | Slow (O(n)) |
| Insert/Delete | Slow | Fast |
| Memory Usage | Compact | More overhead |

---

## 🗝️ 12. Hashtable
- Thread-safe, synchronized.
- Doesn’t allow null keys/values.
- Slower than HashMap.

---

## 🗂️ 13. HashMap vs HashSet
| Feature | HashMap | HashSet |
|----------|----------|----------|
| Structure | Key-Value pair | Unique elements only |
| Allows Null | One null key | One null element |
| Internally Uses | Buckets | HashMap internally |

---

## 🚧 14. Fail-Fast vs Fail-Safe
| Type | Behavior | Example |
|-------|-----------|----------|
| **Fail-Fast** | Throws `ConcurrentModificationException` | ArrayList, HashMap |
| **Fail-Safe** | Works on cloned copy | CopyOnWriteArrayList, ConcurrentHashMap |

---

## ⚖️ 15. Comparator vs Comparable
| Feature | Comparable | Comparator |
|----------|-------------|-------------|
| Package | java.lang | java.util |
| Method | compareTo() | compare() |
| Sorting Type | Natural order | Custom order |
| Example | `class Emp implements Comparable<Emp>` | `Comparator<Emp> byName` |

---

## ⚙️ 16. Consumer vs Producer
- **Producer** → Generates data.
- **Consumer** → Processes data.
```java
Consumer<String> printer = msg -> System.out.println(msg);
printer.accept("Hello Java");
```

---

## 🔁 17. Diamond Problem
Occurs due to multiple inheritance via interfaces:
```java
interface A { default void show() { System.out.println("A"); } }
interface B { default void show() { System.out.println("B"); } }
class C implements A, B {
    public void show() { A.super.show(); }
}
```

---

## 🧵 18. Create Thread
```java
Thread t = new Thread(() -> System.out.println("Running thread..."));
t.start();
```
Or extend `Thread` class.

---

## 🛑 19. Stop Main Thread
- All threads finish
- `System.exit(0)`
- Uncaught exception

---

## ⚡ 20. ConcurrentModificationException
Occurs when modifying a collection while iterating.
```java
for (String s : list) {
    list.remove(s); // Throws exception
}
```
✅ Fix using `Iterator.remove()` or `CopyOnWriteArrayList`.

---

## 🔒 21. Deadlock
Occurs when two threads wait on each other’s lock.
```java
synchronized(obj1) {
    synchronized(obj2) { }
}
```
💡 Avoid by consistent lock order.

---

## 🧠 22. Parallel Threading
Use multiple cores:
```java
list.parallelStream().forEach(System.out::println);
```
Or use `ExecutorService`.

---

## ⏱️ 23. join(), sleep(), yield()
| Method | Description |
|---------|--------------|
| **join()** | Waits for another thread to finish |
| **sleep()** | Pauses current thread temporarily |
| **yield()** | Suggests scheduler to switch threads |

---

## 🧩 24. ExecutorService
Thread pool manager:
```java
ExecutorService es = Executors.newFixedThreadPool(3);
es.submit(() -> System.out.println("Task running..."));
es.shutdown();
```
**Types:** Fixed, Cached, Scheduled, SingleThread.

---

## 🔄 25. Circular Dependency (Spring)
Occurs when two beans depend on each other:
```java
class A { @Autowired B b; }
class B { @Autowired A a; }
```
💡 Fix with `@Lazy` or redesign dependencies.

---

## 🧰 26. Runnable vs Closeable
| Interface | Purpose | Method |
|------------|----------|----------|
| **Runnable** | Defines a thread task | `run()` |
| **Closeable** | Releases resources | `close()` |

---

## ⚙️ 27. CompletableFuture
Used for asynchronous programming:
```java
CompletableFuture.supplyAsync(() -> "Hi")
                 .thenApply(msg -> msg + " there!")
                 .thenAccept(System.out::println);
```

---

## 🧮 28. Threads in ExecutorService
Determined by pool type and CPU cores.
```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available cores: " + cores);
```

