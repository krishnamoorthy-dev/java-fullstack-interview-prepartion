# 🧠 DSA & Java Snippets

A collection of common Data Structures and Algorithm problems solved in Java.

---

## 📦 Arrays

### 1. Merge Two Sorted Arrays

Merges two sorted arrays `nums1` and `nums2` in-place into `nums1` using a **two-pointer approach from the end**.

**Time Complexity:** `O(m + n)` | **Space Complexity:** `O(1)`

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1;
    int j = n - 1;
    int k = (m + n) - 1;
    while (j >= 0) {
        if (i >= 0 && nums1[i] > nums2[j]) {
            nums1[k--] = nums1[i--];
        } else {
            nums1[k--] = nums2[j--];
        }
    }
}
```

**How it works:**
- Start filling `nums1` from the last position.
- Compare elements from the end of both arrays and place the larger one at position `k`.
- Continue until all elements of `nums2` are placed.

---

## 🗂️ LinkedHashMap

### 1. Find First Non-Repetitive Character

Finds the **first character** in a string that appears exactly once, using Java Streams and `LinkedHashMap` to preserve insertion order.

**Time Complexity:** `O(n)` | **Space Complexity:** `O(n)`

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

**How it works:**
- Stream each character and group them by frequency using `Collectors.groupingBy`.
- `LinkedHashMap::new` ensures insertion order is maintained.
- Filter entries with count `== 1` and return the first match.

---

## 📚 Stack

### 1. Next Greater Element

For each element in the array, finds the **next greater element** to its right using a **monotonic stack**.

**Time Complexity:** `O(n)` | **Space Complexity:** `O(n)`

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

**How it works:**
- Traverse the array from **right to left**.
- Maintain a stack of potential "next greater" candidates.
- Pop elements from the stack that are smaller than or equal to the current element.
- The top of the stack (if non-empty) is the next greater element for the current index.

**Output:**
| Element | Next Greater |
|---------|-------------|
| 4       | 5           |
| 5       | 25          |
| 2       | 25          |
| 25      | None        |

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
