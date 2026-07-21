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
1. Every recursive function needs a base case (to stop) and a recursive call (to progress toward that base case) missing a proper base case causes infinite recursion
2. The order of statements relative to the recursive call changes the output order (print-before vs print-after the call)
3. Recursive thinking means trusting that a smaller version of the problem is already solved, then building the full answer from that
4. Backtracking extends recursion by exploring every possible choice, undoing any choice that leads to a dead end, and trying alternatives

### 1. Problem: Print Numbers from N down to 1
```java
public class PrintNToOne {
    public static void main(String[] args) {
        printNumbers(5);
    }

    public static void printNumbers(int n) {
        if (n == 0) {
            return;
        }
        System.out.println(n);
        printNumbers(n - 1);
    }
}
```
Instead of using a loop, this function solves the problem by calling itself with a smaller number each time. We start by calling printNumbers(5). Since 5 isn't 0, we print it, then immediately call printNumbers(4) which prints 4, then calls printNumbers(3) and so on, all the way down.
Eventually we call printNumbers(0). At that point, our stopping condition (n == 0) kicks in, and the function just returns without doing anything else this is what stops the chain from continuing forever.
Since we print the number before making the next call, each number appears on screen the moment we reach it, counting down.

**Output:** 5 4 3 2 1

### 2. Problem: Print Numbers from 1 to N
```java
public class PrintOneToN {
    public static void main(String[] args) {
        printNumbers(5);
    }

    public static void printNumbers(int n) {
        if (n == 0) {
            return;
        }
        printNumbers(n - 1);
        System.out.println(n);
    }
}
```
This looks almost identical to the previous program, but we moved the print statement to happen after the recursive call instead of before it. This one small change completely reverses the output order.
Here's why: when we call printNumbers(5), the very first thing it does is call printNumbers(4) before printing anything. That call then immediately calls printNumbers(3), which calls printNumbers(2), and so on, all the way down to printNumbers(0), which stops.

Only once we hit that stopping point does anything start printing and it prints in reverse order of how the calls were made, starting with whichever call is "closest" to finishing (which was printNumbers(1)), then working back up to the original printNumbers(5) call.

**Output:** 1 2 3 4 5

The big lesson here: where you place code relative to the recursive call before it or after it completely changes when that code actually runs.

### 3. Problem: Sum of First N Numbers
```java
public class SumOfNNumbers {
    public static void main(String[] args) {
        int n = 5;
        int result = sum(n);
        System.out.println("Sum: " + result);
    }

    public static int sum(int n) {
        if (n == 1) {
            return 1;
        }
        return n + sum(n - 1);
    }
}
```
We want to add up all numbers from 1 to 5. Instead of using a loop with a running total, we describe the problem in terms of a smaller version of itself: "the sum of numbers up to 5" is just "5 plus the sum of numbers up to 4." And "the sum up to 4" is just "4 plus the sum up to 3." This keeps shrinking until we reach "the sum up to 1," which is simply 1 no more shrinking needed, that's our base case.

Once we hit that base case, the answers start combining back together: 1, then 2+1=3, then 3+3=6, then 4+6=10, then 5+10=15.

**Output:** Sum: 15

### 4. Problem: Factorial Using Recursion
```java
public class FactorialRecursion {
    public static void main(String[] args) {
        int n = 5;
        System.out.println("Factorial: " + factorial(n));
    }

    public static int factorial(int n) {
        if (n == 0 || n == 1) {
            return 1;
        }
        return n * factorial(n - 1);
    }
}
```
Factorial of 5 (written 5!) means 5 × 4 × 3 × 2 × 1. This code describes that same idea recursively: "factorial of 5" is just "5 multiplied by the factorial of 4," and "factorial of 4" is "4 multiplied by the factorial of 3," and so on shrinking down until we reach factorial of 1 (or 0), which is simply 1 by definition, no further multiplication needed.

Once that base case is hit, the multiplications combine back together on the way up: 1, then 2×1=2, then 3×2=6, then 4×6=24, then 5×24=120.

**Output:** Factorial: 120

### 5. Problem: Power of a Number
```java
public class PowerRecursion {
    public static void main(String[] args) {
        int a = 2, b = 5;
        System.out.println(a + "^" + b + " = " + power(a, b));
    }

    public static int power(int a, int b) {
        if (b == 0) {
            return 1;
        }
        return a * power(a, b - 1);
    }
}
```
We want to calculate 2 raised to the power 5 (2⁵). The base number (a = 2) stays fixed the whole time, while the exponent (b) is what shrinks with each recursive call. "2 to the power 5" is just "2 multiplied by 2 to the power 4," which is "2 multiplied by (2 multiplied by 2 to the power 3)," and so on, until we reach "2 to the power 0" and anything raised to the power 0 is just 1, by definition. That's our base case.

Once that's hit, the multiplications stack back together: 1, then 2×1=2, then 2×2=4, then 2×4=8, then 2×8=16, then 2×16=32.

**Output:** 2^5 = 32

### 6. Problem: Fibonacci Series
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
            return 0;
        }
        if (n == 1) {
            return 1;
        }
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```
The Fibonacci sequence is a pattern where each number is the sum of the two numbers before it (0, 1, 1, 2, 3, 5, 8...). This code has two base cases instead of one: if we're asked for position 0, the answer is just 0. If we're asked for position 1, the answer is just 1. For anything beyond that, we describe it as "the Fibonacci of the previous position, plus the Fibonacci of the position before that" which means the function ends up calling itself twice for every position beyond 1, branching out like a tree, until every branch eventually reaches one of the two base cases.

**Output:** 0 1 1 2 3 5 8 13 21 34

### 7. Problem: Reverse a String Using Recursion
```java
public class ReverseStringRecursion {
    public static void main(String[] args) {
        String str = "java";
        reverse(str);
    }

    public static void reverse(String str) {
        if (str.length() == 0) {
            return;
        }
        System.out.print(str.charAt(str.length() - 1));
        reverse(str.substring(0, str.length() - 1));
    }
}
```
Each time this function runs, it does two things: it prints the very last character of whatever string it currently has, and then it calls itself again with a slightly shorter version of the string — one character shorter, with that last character chopped off.

So for "java": first it prints the last letter, a, then calls itself with "jav". That call prints the last letter of "jav", which is v, then calls itself with "ja". That prints a, then calls with "j". That prints j, then calls with an empty string — which triggers the base case, and the recursion stops.

Since we print the last character before shrinking the string each time, the letters come out in reverse order automatically.

**Output:** avaj

### 8. Problem: Count Digits Using Recursion
```java
public class CountDigitsRecursion {
    public static void main(String[] args) {
        int num = 12345;
        System.out.println("Number of digits: " + countDigits(num));
    }

    public static int countDigits(int num) {
        if (num == 0) {
            return 0;
        }
        return 1 + countDigits(num / 10);
    }
}
```
Dividing a number by 10 (using whole-number division) chops off its last digit. For example, 12345 / 10 gives 1234 (the 5 gets dropped). This code uses that trick: every time it calls itself, it removes one digit from the number and adds 1 to a running count — until the number eventually shrinks all the way down to 0, meaning there are no digits left to count.

Tracing through 12345: count 1 digit + look at 1234 → count 1 more + look at 123 → count 1 more + look at 12 → count 1 more + look at 1 → count 1 more + look at 0 → stop. Total: 5 digits counted.

**Output:** Number of digits: 5

### 9. Problem: Backtracking: Generate All Binary Strings of Length N
```java
public class GenerateBinaryStrings {
    public static void main(String[] args) {
        generate("", 3);
    }

    public static void generate(String current, int n) {
        if (current.length() == n) {
            System.out.println(current);
            return;
        }
        generate(current + "0", n);
        generate(current + "1", n);
    }
}
```
We want every possible combination of 0s and 1s that's exactly 3 characters long. We start with an empty string and build it up one character at a time. At every single position, we have two choices: add a 0, or add a 1. Instead of picking just one, we try both calling the function once for each choice, so every possible path gets explored.

Once our string reaches the target length (3 characters), that's a complete, valid combination, so we print it and stop building further on that particular path. Because we tried both choices at every step, all 2 × 2 × 2 = 8 possible combinations eventually get generated and printed.

**Output:**
000
001
010
011
100
101
110
111

**Why is this called backtracking, not just recursion?**
Because at every step, we're exploring every possible branch (both the "add 0" path and the "add 1" path), not just following one single path down to a single answer that's the defining trait of backtracking versus plain recursion.

### 10. problem: Backtracking: Generate All Subsets of a String
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

        generateSubsets(str, current, index + 1);
        generateSubsets(str, current + str.charAt(index), index + 1);
    }
}
```
For a word like "abc", we want every possible smaller combination you could make by picking any subset of its letters including picking none of them, and including picking all of them.

We walk through the word one letter at a time (tracked by index). At each letter, we have exactly two choices: skip it (leave it out of our current combination) or include it (add it onto our current combination). Just like the binary string example, instead of picking only one choice, we try both by calling the function twice once for "skip this letter," once for "include this letter."

Once we've made a decision (skip or include) for every letter in the word, index reaches the end of the string, and whatever combination we built along that particular path gets printed as one valid subset.

**Output:** (empty set), c, b, bc, a, ac, ab, abc

Short Notes:

1. Recursion solves a problem by describing it in terms of a smaller version of itself, always with a base case that stops the chain
2. The order of code around the recursive call matters placing something before vs after the call changes exactly when it runs
3. Recursive thinking means trusting that the smaller sub-problem is already solved, and just figuring out how to combine that with your current step
4. Backtracking takes recursion further instead of following just one path, it tries every possible choice at each step, which is why it's the go-to technique for "generate all possibilities" type problems




