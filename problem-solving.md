# 🧠 DSA & Java Snippets

A collection of common Data Structures and Algorithm problems solved in Java.

---

## 🛠️ Prerequisites

- Java 8+
- Basic understanding of Arrays, LinkedHashMap, and Stack

---

## 📁 Topics Covered

| Topic         | Problem                          |
|---------------|----------------------------------|
| Arrays        | Merge Two Sorted Arrays          |
| LinkedHashMap | First Non-Repetitive Character   |
| Stack         | Next Greater Element             |


## 📦 Arrays

### 1. Merge Two Sorted Arrays

```java
// Merge two sorted array in nature order
        int a[] = {1,3,4,5,6,8};
        int b[] = {1,2,4,6,7};
        
        int i = 0;
        int j = 0;
        int k = 0;
        int result[] = new int[a.length+b.length];
        
        while(k < (a.length+b.length)) {
            if(i < a.length && j < b.length && a[i] > b[j]) {
                result[k] = b[j++];
            } else if(i < a.length) {
                result[k] = a[i++];
            } else if(j < b.length) {
                result[k] = b[j++];
            }
            System.out.print(result[k]);
            k++;
        }
```
Output: 11234456678

### 2. Group by string first letter

```java
        String fruites[] = {"orange", "apple","banna","grapes","mango","avocado"};
        Arrays.stream(fruites).collect(Collectors.groupingBy( fruite -> fruite.charAt(0))).forEach( (key, value) -> System.out.print(key+"=>"+value));
```
Output: a=>[apple, avocado]b=>[banna]g=>[grapes]m=>[mango]o=>[orange]

### 3. Find the longest string in a array of strings

```java
        String fruites[] = {"orange", "apple","banna","grapes","mango","avocado"};
        String maxLenStr = Arrays.stream(fruites).max(Comparator.comparingInt(String::length)).orElse("");
        System.out.print(maxLenStr);
```
Output: avocado

---

## 🗂️ LinkedHashMap

### 1. Find First Non-Repetitive Character

```java
public static void main(String[] args) {
    String input = "coconut";

    Character result = input.chars()
        .mapToObj(a -> (char) a)
        .collect(Collectors.groupingBy(
            Function.identity(),
            LinkedHashMap::new,
            Collectors.counting()
        ))
        .entrySet().stream()
        .filter(a -> a.getValue() == 1)
        .map(a -> a.getKey())
        .findFirst()
        .get();

    System.out.println(result); // Output: u
}
```

---

## 📚 Stack

### 1. Next Greater Element

```java
public static void main(String[] args) {
    int[] a = {4, 5, 2, 25};
    var container = new Stack<Integer>();

    for (int i = a.length - 1; i >= 0; i--) {
        while (!container.isEmpty() && container.peek() <= a[i]) {
            container.pop();
        }
        if (!container.isEmpty()) {
            System.out.println(container.peek());
        }
        container.push(a[i]);
    }
}
```

**Output:**
| Element | Next Greater |
|---------|-------------|
| 4       | 5           |
| 5       | 25          |
| 2       | 25          |
| 25      | None        |

---
