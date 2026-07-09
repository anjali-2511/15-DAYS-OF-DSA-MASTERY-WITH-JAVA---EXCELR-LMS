# Day 02 — Arrays Basics, Array Operations, Linear Search & Basic Array Problems
Topics:

### 1. Arrays Basics
### 2. Array Operations
### 3. Linear Search
### 4. Basic Array Problems

## 1. Arrays Basics

**What is an Array?**
An array is a linear data structure a collection of elements of the same data type, stored in contiguous memory locations, and accessed using an index.

In simple words: a single variable that can store multiple values of the same type.

**Analogy:** Imagine a classroom with 10 students. Instead of writing each student's attendance in a separate notebook, you use one attendance register — that register works like an array, holding all the records together in one organized place.

**Why do we need arrays?**
If you had to store marks for 5 students, declaring 5 separate variables gets messy — and completely unmanageable if there are 100 or 1,000 students. Arrays solve this by storing all values together, accessible by index.

**Characteristics of Arrays:**

1. Stores elements of the same data type
2. Stored in contiguous memory
3. Has a fixed size (this becomes a drawback later — arrays can't grow dynamically)
4. Uses indexing for fast random access

**Advantages:**

1. Easy to store
2. Easy to access
3. Easy to update
4. Easy to traverse (using a loop)
5. Scalable to a fixed limit

### Declaring, taking input, and printing an array (Java):
```java
import java.util.Scanner;

public class DemoArray {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int arr[] = new int[5]; // declaring array of size 5

        // taking input from user
        for (int i = 0; i < arr.length; i++) {
            System.out.println("Enter the " + i + "th value: ");
            arr[i] = sc.nextInt();
        }

        // printing the array
        for (int i = 0; i < arr.length; i++) {
            System.out.println("arr[" + i + "] = " + arr[i]);
        }
    }
}
```

## 2. Array Operations

Array operations are actions performed on an array: creating, inserting, traversing, accessing, updating, searching, deleting, sorting, merging, reversing, finding max/min, etc.

**Accessing a specific element**
### You can access any element directly using its index:
```java
System.out.println(arr[2]); // prints the element at index 2 (3rd position)
```
### Updating an element
```java
public class UpdateArray {
    public static void main(String[] args) {
        int arr[] = {10, 20, 30, 40, 50};

        arr[2] = 100; // updating the value at index 2 (was 30, now 100)

        // enhanced for loop to print
        for (int num : arr) {
            System.out.println(num);
        }
    }
}
```
The enhanced for-loop (for (int num : arr)) automatically picks each value from the array one at a time and stores it in num a shorter way to traverse without managing an index manually.

**Inserting an element at a specific position**

### This is trickier you need to shift elements to the right first to make space, starting from the end of the array (not the beginning).
```java
public class InsertArray {
    public static void main(String[] args) {
        int arr[] = new int[6]; // extra space reserved for the new element
        arr[0] = 10;
        arr[1] = 20;
        arr[2] = 30;
        arr[3] = 40;
        arr[4] = 50;

        int position = 2;   // where we want to insert
        int value = 25;     // value to insert

        // shift elements to the right, starting from the last index
        for (int i = 4; i >= position; i--) {
            arr[i + 1] = arr[i];
        }

        arr[position] = value; // insert the new value

        for (int num : arr) {
            System.out.println(num);
        }
    }
}
```
Why start from the end? Picture the array as boxes in a row: 1, 7, 10, 11, 15 with one empty box at the end. To insert 8 at position 2, you shift 15 → last box, 11 → next, 10 → next, opening up a gap at position 2 for 8. If you shifted from the front instead, you'd overwrite values before you could move them — that's why the loop runs backward.

## 3. Linear Search

Linear Search is the simplest searching algorithm it compares the target value with each element of the array one by one, sequentially, starting from the first element, until either the value is found or the array ends.

**Analogy:** Finding a specific seat in a classroom by checking seat 1, then seat 2, then seat 3... one at a time, in order — that's linear search.

**When to use Linear Search:**

1. When the data is unsorted
2. When the dataset is small
3. When simplicity matters more than speed
4. When the array changes frequently (so sorting it each time isn't worth it)

**Time complexity:** O(n) — worst case, you may have to check every element.

### Code:
```java
public class LinearSearchDemo {
    public static void main(String[] args) {
        int arr[] = {10, 20, 30, 40, 50};
        int target = 40;

        int index = linearSearch(arr, target);

        if (index != -1) {
            System.out.println("Element found at index: " + index);
        } else {
            System.out.println("Element not found");
        }
    }

    public static int linearSearch(int arr[], int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return i; // return the index where match is found
            }
        }
        return -1; // -1 means target wasn't found in the array
    }
}
```
**How it works, step by step:**

**Array:** {10, 20, 30, 40, 50}, indices 0, 1, 2, 3, 4
Target 40 sits at index 3
The loop checks each element from index 0 onward; when arr[i] == target, it returns i
If the loop finishes without a match, it returns -1

**Why static?**
A method is made static so it can be called directly using the class name, without needing to create an object of that class first — it becomes a property of the class itself.

## 4. Basic Array Problems

**General problem-solving strategy (applies to any DSA problem):**

1. Read the problem carefully
2. Understand the input
3. Understand the expected output
4. Think through the logic manually first
5. Write the algorithm (steps) before coding
6. Implement it in Java
7. Test it

### Problem 1: Print All Elements
```java
public class PrintArray {
    public static void main(String[] args) {
        int arr[] = {10, 20, 30, 40};

        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```
We have a box with 4 slots, and each slot has a number: 10, 20, 30, 40. Each slot has a position number (called an index), starting from 0. So slot 0 has 10, slot 1 has 20, slot 2 has 30, slot 3 has 40.
Now we use a loop to visit every slot one by one. We start a counter i at 0. As long as i is less than the total number of slots (4 in this case), we print whatever is in slot number i, and then we move to the next slot by increasing i by 1.

So it goes like this:

1. i is 0 → print slot 0 → prints 10 → move to next
2. i is 1 → print slot 1 → prints 20 → move to next
3. i is 2 → print slot 2 → prints 30 → move to next
4. i is 3 → print slot 3 → prints 40 → move to next
5. i becomes 4 → but we only have slots 0 to 3, so the loop stops here

**Output:** 10, 20, 30, 40 — each on its own line.

### Problem 2: Find the Sum of All Elements
```java
public class SumOfArray {
    public static void main(String[] args) {
        int arr[] = {10, 20, 30, 40};
        int sum = 0;

        for (int num : arr) {
            sum += num;
        }

        System.out.println("Sum: " + sum);
    }
}
```
We want to add up all the numbers in the array. So we create a variable called sum and start it at 0 — think of it like an empty piggy bank.
Then we go through the array one number at a time. Every time we look at a number, we add it into our piggy bank (sum). We keep doing this until we've gone through every number in the array.

So it goes like this:

1. Piggy bank starts empty: 0
2. We see 10, add it in → piggy bank now has 10
3. We see 20, add it in → piggy bank now has 30
4. We see 30, add it in → piggy bank now has 60
5. We see 40, add it in → piggy bank now has 100

By the end, the piggy bank (sum) has 100, which is the total.

**Output:** Sum: 100

**Why does sum remember its value between each loop step?** 
Because we created it outside the loop, before the loop even started. If we had created it inside the loop, it would reset to 0 every single time — like emptying the piggy bank after every coin.










