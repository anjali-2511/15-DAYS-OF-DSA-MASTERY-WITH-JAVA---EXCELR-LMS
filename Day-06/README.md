# Day 06 — Recursion, Recursive Thinking & Backtracking Basics

Topics:

1. Recursion
2. Recursive Thinking
3. Backtracking Basics

## 1. Recursion

Recursion is a programming technique in which a method calls itself repeatedly until a certain condition is met. Instead of using a for or while loop, recursion solves a problem by breaking it into smaller versions of the same problem.

**Analogy:** Imagine standing between two facing mirrors — your reflection keeps appearing again and again, smaller and smaller, endlessly. A recursive function calling itself works the same way — except in code, we need a stopping point, or it would go on forever.

**The two essential parts of every recursive function**
**1. Base case —** the condition that stops the recursion. Without a clear base case, the function will call itself infinitely, eventually crashing the program.
**2. Recursive call —** the part where the function calls itself again, usually with a smaller or simpler input than before.

### Basic structure
```java
returnType functionName(parameters) {
    if (baseCondition) {
        return someValue;      // base case — stops the recursion
    }
    return functionName(smallerInput); // recursive call
}
```
### Example: Print Numbers from N down to 1
```java
public class PrintNToOne {
    public static void main(String[] args) {
        printNumbers(5);
    }

    public static void printNumbers(int n) {
        if (n == 0) {
            return; // base condition
        }
        System.out.println(n);
        printNumbers(n - 1); // recursive call, with a smaller input
    }
}
```
**Output:** 5 4 3 2 1

### Practice task: Print Numbers from 1 to N
(Given as a practice exercise — solved by simply moving the print statement after the recursive call)
```java
public class PrintOneToN {
    public static void main(String[] args) {
        printNumbers(5);
    }

    public static void printNumbers(int n) {
        if (n == 0) {
            return;
        }
        printNumbers(n - 1); // go all the way down first
        System.out.println(n); // then print on the way back up
    }
}
```
**Output:** 1 2 3 4 5

Why does swapping the order of the print statement reverse the output? When the print comes before the recursive call, each number gets printed immediately, in descending order. When the print comes after the recursive call, Java has to finish calling itself all the way down to the base case first and only then, as each call "returns" back up the chain, does the print statement execute, producing the reverse (ascending) order.

### Example: Sum of First N Numbers
```java
public class SumOfNNumbers {
    public static void main(String[] args) {
        int n = 5;
        int result = sum(n);
        System.out.println("Sum: " + result);
    }

    public static int sum(int n) {
        if (n == 1) {
            return 1; // base condition
        }
        return n + sum(n - 1); // recursive call
    }
}
```
**Output:** Sum: 15 (5+4+3+2+1)

### Example: Factorial Using Recursion
```java
public class FactorialRecursion {
    public static void main(String[] args) {
        int n = 5;
        System.out.println("Factorial: " + factorial(n));
    }

    public static int factorial(int n) {
        if (n == 0 || n == 1) {
            return 1; // base condition
        }
        return n * factorial(n - 1); // recursive call
    }
}
```
**Output:** Factorial: 120 (5×4×3×2×1)

### Example: Power of a Number
```java
public class PowerRecursion {
    public static void main(String[] args) {
        int a = 2, b = 5;
        System.out.println(a + "^" + b + " = " + power(a, b));
    }

    public static int power(int a, int b) {
        if (b == 0) {
            return 1; // base condition — anything to the power 0 is 1
        }
        return a * power(a, b - 1); // recursive call
    }
}
```
**Output:** 2^5 = 32 Time complexity: O(n), since the function calls itself b times.

### Example: Fibonacci Series
(Given as a practice task — here's a working solution)
```java
public class FibonacciRecursion {
    public static void main(String[] args) {
        int n = 10;
        for (int i = 0; i < n; i++) {
            System.out.print(fibonacci(i) + " ");
        }
    }

    public static int fibonacci(int n) {
        if (n == 0) {
            return 0; // base condition 1
        }
        if (n == 1) {
            return 1; // base condition 2
        }
        return fibonacci(n - 1) + fibonacci(n - 2); // recursive call
    }
}
```
**Output:** 0 1 1 2 3 5 8 13 21 34

### Example: Reverse a String Using Recursion
```java
public class ReverseStringRecursion {
    public static void main(String[] args) {
        String str = "java";
        reverse(str);
    }

    public static void reverse(String str) {
        if (str.length() == 0) {
            return; // base condition
        }
        System.out.print(str.charAt(str.length() - 1));
        reverse(str.substring(0, str.length() - 1)); // recursive call, with a shorter string
    }
}
```
**Output:** avaj

### Example: Count Digits Using Recursion
```java
public class CountDigitsRecursion {
    public static void main(String[] args) {
        int num = 12345;
        System.out.println("Number of digits: " + countDigits(num));
    }

    public static int countDigits(int num) {
        if (num == 0) {
            return 0; // base condition
        }
        return 1 + countDigits(num / 10); // recursive call, dividing by 10 removes the last digit
    }
}
```
**Output:** Number of digits: 5

