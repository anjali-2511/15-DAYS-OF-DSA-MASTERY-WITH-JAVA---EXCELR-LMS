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





 
