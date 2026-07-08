# Day 01 — Introduction to DSA, Big-O, Java Review & Problem Solving

Topics:
### 1. Introduction to DSA
### 2. Time & Space Complexity (Big O)
### 3. Java Review for DSA
### 4. Problem Solving Approach


## 1. Introduction to DSA:

# DSA = Data Structures + Algorithms

**What is a Data Structure?**
### A way of organizing and storing data so it can be accessed and modified efficiently.
**Analogy:** Imagine a library. If books are thrown randomly on the floor, finding one takes hours. But if books are organized by subject, author, or ISBN number, searching becomes instant. A data structure does the same job for data inside a computer.

**What is an Algorithm?**
### A step-by-step procedure to solve a problem.
**Analogy:** Making tea — boil water → add tea powder → add sugar → add milk → boil → serve. That sequence of steps is an algorithm.
**Code example:** Finding the largest number in a list — start with the first number as "largest," compare it with the next, update if a bigger one is found, repeat till the end, then print the result.
```java
public class LargestNumber {
    public static void main(String[] args) {
        int[] numbers = {12, 45, 3, 67, 22, 89, 5};

        int largest = numbers[0]; // start with the first number

        for (int i = 1; i < numbers.length; i++) {
            if (numbers[i] > largest) {
                largest = numbers[i];
            }
        }

        System.out.println("Largest number: " + largest);
    }
}
```

## Putting it together: 
Data structures store the data, algorithms process it — together they solve problems efficiently. That combination is DSA.

**Why does DSA matter?**
Simply writing code that "works" isn't enough in the software industry. 
**Companies expect code that is:**
1. Fast — runs efficiently
2. Memory-efficient — doesn't waste RAM
3. Scalable — can handle more users/data later without breaking
4. Maintainable — easy to read, update, and extend

**Example:** searching among 10 students manually is easy. Searching through 10 million users manually would be painfully slow — an efficient algorithm can do it in milliseconds.
```java
public class LargestNumber {
    public static void main(String[] args) {
        // Works the same whether you have 10 numbers or 10 million —
        // each number is checked only once, so it's fast even at scale.
        int[] numbers = {12, 45, 3, 67, 22, 89, 5};

        int largest = numbers[0]; // assume first number is the largest initially

        for (int i = 1; i < numbers.length; i++) {
            if (numbers[i] > largest) {
                largest = numbers[i]; // update when a bigger number is found
            }
        }

        System.out.println("Largest number: " + largest);
    }
}
```
**Time complexity:** O(n) — one pass through the list, no matter how large it is.

**Where is DSA actually used?**

**Product-based companies (Google, Microsoft, Amazon, Meta, Apple, Adobe, Oracle, Salesforce, Atlassian) —**  heavily test DSA in interviews

**Service-based companies —** increasingly ask DSA questions too, not just product companies

**Real-world domains:**
1. Banking → transaction processing, fraud detection
2. E-commerce → product search, recommendations
3. Social media → friend suggestions, feed ranking
4. Healthcare → patient records, scheduling
5. Gaming → pathfinding, AI opponents
6. Cybersecurity → encryption, pattern matching
7. Cloud computing → resource scheduling, caching
8. Data science/AI → data processing, optimization, graph search


## 2. Time & Space Complexity (Big O)

### Time Complexity
Measures how the execution time of an algorithm grows as input size increases — it does not measure actual seconds; it measures the growth rate.

Why ignore actual seconds? Because the same algorithm might take 1 second on one computer and 0.5 seconds on a faster one — the algorithm itself hasn't changed. So we measure number of operations, not wall-clock time.

**Why it matters:** If two developers solve the same problem differently, time complexity tells you objectively which solution is more efficient.

**What is "n"?**
In DSA, n represents the input size — instead of writing the actual number (10, 1000, 1 million), we generalize it as n.

**Big O Notation**
Tells us how running time increases as input size increases. It ignores CPU speed, RAM, and programming language it only measures algorithm efficiency.

NotationNameExampleO(1)ConstantAccessing the first element of an array (same speed regardless of array size) — e.g. ATM balance checkO(log n)LogarithmicBinary search — like opening the middle page of a dictionary instead of checking page by pageO(n)LinearLooping through all elements once (linear search)O(n log n)LinearithmicEfficient sorting algorithmsO(n²)QuadraticNested loopsO(2ⁿ)ExponentialVery inefficient recursive solutions

**Growth order (fastest → slowest):**
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ)

### Space Complexity
Measures how much extra memory an algorithm needs as input size grows includes variables, arrays, objects, function calls, and recursion stack usage.

-> **O(1) space:** using a single variable (e.g. a sum variable) regardless of input size
-> **O(n) space:** creating an array/structure whose size grows with the input (e.g. array size = n)

### Time vs Space Trade-off
Sometimes we use more memory to save time.

**Example:** If you don't save a contact's number in your phone, finding it later means searching manually (slow). If you save it (uses memory), retrieving it is instant.

**Code example:** Searching for an element without a HashMap takes O(n) time. Storing values in a HashMap first takes extra memory, but then searching becomes O(1) — instant.
```java
public class SimpleSearch {
    public static void main(String[] args) {
        int[] numbers = {12, 45, 3, 67, 22, 89, 5};
        int target = 67;

        boolean found = false;

        for (int i = 0; i < numbers.length; i++) {
            if (numbers[i] == target) {
                found = true;
                break; // stop as soon as we find it
            }
        }

        if (found) {
            System.out.println(target + " was found in the list.");
        } else {
            System.out.println(target + " was not found.");
        }
    }
}
```

### Quick rules for calculating time complexity:

1. Single statement → O(1)
2. Single loop → O(n)
3. Nested loop → O(n²)
4. Loop that halves the search space each time (like binary search) → O(log n)

**Key takeaway:** Lower complexity generally means better scalability. In interviews and real engineering work, choosing the right algorithm/data structure matters more than just writing more lines of code.


## 3. Java Review for DSA

Before we start implementing data structures in Java, make sure you're comfortable with these basics:

1. Classes & main method
2. Variables & data types
3. Arrays
4. Loops (for, while)
5. Conditional statements (if/else)
6. Output statements (System.out.println)
7. Basic idea of the Java Collections Framework (helps solve most DSA problems efficiently we'll use this a lot going forward)

Basic Java program structure:
```java
public class DemoFirst {
    public static void main(String[] args) {
        System.out.println("Welcome to session");
    }
}
```

## 4. Problem Solving Approach

This part was only briefly introduced today — the instructor mentioned that Day 1 was a concept-only/theory session, and hands-on coding + actual problem-solving starts from Day 2 onward. So don't worry if you haven't solved any problems yet — that's expected at this stage.

### Key Takeaways:

**DSA** = Data Structures (how we store data) + Algorithms (how we process it)
**Good code isn't just "working" code —** it must be fast, memory-efficient, scalable, and maintainable
**Time complexity =** how execution time grows with input size (measured in operations, not seconds)
**Space complexity =** how much extra memory is needed as input grows
Sometimes we trade memory for speed (time vs space trade-off)
Java basics (classes, loops, arrays, collections) are the foundation for implementing DSA concepts.
 







 
