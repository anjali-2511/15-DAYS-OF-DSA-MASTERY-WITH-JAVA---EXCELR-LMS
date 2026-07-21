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


## 2. Recursive Thinking

Recursive thinking is the ability to solve a large problem by breaking it into a smaller problem of the same type, repeating this until the problem becomes small enough to solve directly (the base case).

**Analogy (stairs):** Instead of figuring out how to climb 5 stairs all at once, you just think about climbing one stair at a time — solving the same small problem repeatedly until you reach the top.

**Analogy (nesting dolls):** Big doll → medium doll → small doll → tiny doll → no more doll. Each doll contains a smaller version of the same problem, until you reach the smallest one (the base case) where there's nothing left to open.

The general recursive thinking process:
1. What is the smallest version of this problem? (this becomes your base case)
2. Assume the smaller version of the problem is already solved
3. Combine that smaller solution with the current step to build the full answer

Every recursive example covered above (printing numbers, sum, factorial, power, Fibonacci, string reversal, digit counting) is an application of this same recursive thinking pattern each one breaks a bigger problem into a smaller version of itself.

## 3. Backtracking Basics

Backtracking is an algorithmic technique that builds a solution step by step. If a choice made along the way leads to an invalid or dead-end solution, the algorithm undoes that choice (backtracks) and tries a different path instead.

**Analogy:** Imagine you're in a maze trying to reach the exit. You try going right it's blocked. You backtrack, then try going left that path continues, so you keep going. If that too hits a dead end, you backtrack again and try another direction, until you eventually reach the exit.

### Recursion vs Backtracking:

| Aspect | Recursion | Backtracking |
|--------|-----------|--------------|
| Goal | Solves smaller sub-problems | Explores **all possible** solutions |
| Undoing work | Doesn't necessarily undo anything | Always undoes the previous choice when a path fails |
| Answers returned | Usually returns one answer | Can return one or many answers |

### General backtracking algorithm pattern
```java
function solve(problem):
    if solution found:
        print/save the solution
        return
    for each possible choice:
        make a choice
        solve(smaller/similar problem)
        undo the choice (backtrack)
```
### Example: Generate All Binary Strings of Length N
```java
public class GenerateBinaryStrings {
    public static void main(String[] args) {
        generate("", 3);
    }

    public static void generate(String current, int n) {
        if (current.length() == n) {
            System.out.println(current); // base condition: solution complete
            return;
        }
        generate(current + "0", n); // choice 1: add a '0'
        generate(current + "1", n); // choice 2: add a '1'
    }
}
```
**Output (for n = 3):**
000
001
010
011
100
101
110
111

### Example: Generate All Subsets of a String
(Given as a practice task here's a working solution)
```java
public class GenerateSubsets {
    public static void main(String[] args) {
        String str = "abc";
        generateSubsets(str, "", 0);
    }

    public static void generateSubsets(String str, String current, int index) {
        if (index == str.length()) {
            System.out.println(current.isEmpty() ? "(empty set)" : current);
            return;
        }

        // choice 1: exclude the current character
        generateSubsets(str, current, index + 1);

        // choice 2: include the current character
        generateSubsets(str, current + str.charAt(index), index + 1);
    }
}
```
**Output (for "abc"):** (empty set), c, b, bc, a, ac, ab, abc

Real-world applications of backtracking:
1. Solving mazes and pathfinding problems
2. Sudoku solvers
3. Undoing choices in an operating system deadlock situation
4. Generating combinations/permutations (like the examples above)

Key Notes:
1. Every recursive function needs a base case (to stop) and a recursive call (to progress toward that base case) — missing a proper base case causes infinite recursion
2. The order of statements relative to the recursive call changes the output order (print-before vs print-after the call)
3. Recursive thinking means trusting that a smaller version of the problem is already solved, then building the full answer from that
4. Backtracking extends recursion by exploring every possible choice, undoing any choice that leads to a dead end, and trying alternatives

