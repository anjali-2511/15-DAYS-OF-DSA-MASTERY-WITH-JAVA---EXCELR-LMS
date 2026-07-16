# Day 04 — Sorting Algorithms (Bubble, Selection, Insertion Sort)

Topics:

1. Purpose of Sorting
2. Java's Built-in Sort Method
3. Bubble Sort
4. Selection Sort
5. Insertion Sort
6. Sorting Complexity


## 1. Purpose of Sorting

**Why Do We Need Sorting?**
Sorting means arranging data in a particular order either ascending (smallest to largest) or descending (largest to smallest).

Sorting is one of the most important concepts in DSA because many efficient algorithms like Binary Search require the data to already be sorted before they can work.

Real-world reasons we sort data:

1. Finding the highest/lowest value instantly (e.g. topper's marks, lowest score)
2. Calculating rankings easily
3. Enabling binary search which doesn't work on unsorted data
4. Generating clean, ordered reports

Real-world examples:

1. E-commerce: sorting products by price, rating, or popularity
2. Banking: sorting transactions by date or amount
3. Hospitals: sorting patients by priority

### Types of Sorting Algorithms
Sorting algorithms are broadly classified into two categories:

1. Comparison-based sorting — compares elements directly to decide their order. Examples: Bubble Sort, Selection Sort, Insertion Sort, Merge Sort, Quick Sort
2. Non-comparison-based sorting — doesn't compare elements directly. Examples: Counting Sort, Radix Sort, Bucket Sort

## 2. Java's Built-in Sort Method

Before writing your own sorting logic, it's worth knowing Java already provides a ready-made sort() method via the Arrays class.
```java
import java.util.Arrays;

public class SortDemo {
    public static void main(String[] args) {
        int arr[] = {40, 10, 30, 20};

        Arrays.sort(arr); // sorts the array in ascending order, in place

        for (int num : arr) {
            System.out.println(num);
        }
    }
}
```
Why do we need to import java.util.Arrays? The sort() method belongs to the Arrays class, which lives in the java.util package so we must import it before we can use it.

**Output:**
10
20
30
40

This built-in method is great for real projects, but in interviews and for learning DSA, you're expected to know how sorting actually works underneath which is exactly what Bubble, Selection, and Insertion Sort teach you.

## 3. Bubble Sort

Bubble Sort is the simplest sorting algorithm. It repeatedly compares two adjacent elements and swaps them if they're in the wrong order. After each full pass through the array, the largest unsorted element "bubbles up" to its correct position at the end hence the name.

**Analogy:** Imagine comparing the heights of students standing in a line, two at a time, swapping them if the shorter one is standing after the taller one. After going down the line once, the tallest student ends up at the very end. Repeat this process, and eventually everyone is arranged shortest to tallest.

Code:
```java
import java.util.Arrays;

public class BubbleSort {
    public static void main(String[] args) {
        int arr[] = {5, 3, 8, 4, 2};
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {         // controls number of passes
            for (int j = 0; j < n - i - 1; j++) {  // compares adjacent elements
                if (arr[j] > arr[j + 1]) {
                    // swap
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }

        System.out.println("Sorted array: " + Arrays.toString(arr));
    }
}
```
**Why n - i - 1 in the inner loop?**
After each pass, the largest remaining element has already bubbled to its correct final position at the end so there's no need to keep comparing that already-sorted portion again. Each pass, the inner loop's range shrinks by 1.

**Optimization:** Stop early if already sorted

If a pass completes with no swaps, the array is already fully sorted no need to continue further passes. This is done using a boolean "swap flag":
```java
public class BubbleSortOptimized {
    public static void main(String[] args) {
        int arr[] = {5, 3, 8, 4, 2};
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;

            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }

            if (!swapped) {
                break; // no swaps happened, array is already sorted, stop early
            }
        }

        System.out.println("Sorted array: " + java.util.Arrays.toString(arr));
    }
}
```
Assignment given: Display the array after each pass
```java
public class BubbleSortShowPasses {
    public static void main(String[] args) {
        int arr[] = {5, 3, 8, 4, 2};
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }

            System.out.println("After pass " + (i + 1) + ": " + java.util.Arrays.toString(arr));
        }
    }
}
```

## 4. Selection Sort

Selection Sort repeatedly finds the smallest element from the unsorted part of the array and places it at the beginning of the unsorted section. Unlike Bubble Sort (which does many swaps per pass), Selection Sort does only one swap per pass.

**Analogy:** A teacher arranging students by height finds the shortest student, moves them to position 1, then finds the next shortest among the rest, moves them to position 2, and repeats until everyone is arranged.

Code (Ascending order):
```java
public class SelectionSort {
    public static void main(String[] args) {
        int arr[] = {64, 25, 12, 22, 11};
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {
            int minIndex = i; // assume current position holds the minimum

            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j; // found a smaller element, update minIndex
                }
            }

            // swap the found minimum with the first unsorted position
            int temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
        }

        System.out.println("Sorted array (ascending): " + java.util.Arrays.toString(arr));
    }
}
```
Code (Descending order):
Only the comparison changes everything else stays the same:
```java
public class SelectionSortDescending {
    public static void main(String[] args) {
        int arr[] = {64, 25, 12, 22, 11};
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {
            int maxIndex = i;

            for (int j = i + 1; j < n; j++) {
                if (arr[j] > arr[maxIndex]) { // only this comparison flipped
                    maxIndex = j;
                }
            }

            int temp = arr[maxIndex];
            arr[maxIndex] = arr[i];
            arr[i] = temp;
        }

        System.out.println("Sorted array (descending): " + java.util.Arrays.toString(arr));
    }
}
```
**Optimization:** Avoid unnecessary swaps

If the minimum element found is already in the correct position, skip the swap entirely:
```java
public class SelectionSortOptimized {
    public static void main(String[] args) {
        int arr[] = {64, 25, 12, 22, 11};
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;

            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }

            if (minIndex != i) { // only swap if a genuinely smaller element was found elsewhere
                int temp = arr[minIndex];
                arr[minIndex] = arr[i];
                arr[i] = temp;
            }
        }

        System.out.println("Sorted array: " + java.util.Arrays.toString(arr));
    }
}
```


## 5. Insertion Sort

Insertion Sort builds the sorted array one element at a time. It takes each element from the unsorted portion and inserts it into its correct position within the already-sorted portion (on its left).

**Analogy:** Imagine sorting playing cards in your hand as you're dealt them, one at a time. You receive a 7 — it's alone, so it's "sorted." You receive a 5 — you slide it in before the 7. You receive a 9 — you place it after the 7. You receive a 6 — you shift the 7 and 9 over to make room and insert 6 in the correct spot. By the end, your whole hand is sorted, one card at a time.

Code (Ascending order):
```java
public class InsertionSort {
    public static void main(String[] args) {
        int arr[] = {5, 2, 4, 6, 1, 3};
        int n = arr.length;

        for (int i = 1; i < n; i++) {
            int key = arr[i];      // the element we're trying to place correctly
            int j = i - 1;

            // shift elements bigger than key one position to the right
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            arr[j + 1] = key; // insert key into its correct position
        }

        System.out.println("Sorted array: " + java.util.Arrays.toString(arr));
    }
}
```
**Why start from index 1, not 0?** 
A single element (arr[0]) is always "sorted" by itself there's nothing to compare it to yet. So we start building the sorted section from the second element onward.


## 6. Sorting Complexity

Sorting complexity refers to the time and memory required by a sorting algorithm to arrange data.

| Algorithm      | Best Case                  | Average Case | Worst Case | Space Complexity |
|----------------|-----------------------------|---------------|-------------|-------------------|
| Bubble Sort    | O(n) *(with optimization)*  | O(n²)         | O(n²)       | O(1)              |
| Selection Sort | O(n²)                       | O(n²)         | O(n²)       | O(1)              |
| Insertion Sort | O(n) *(already sorted)*     | O(n²)         | O(n²)       | O(1)              |

**Key observation:** All three basic sorting algorithms have O(n²) time complexity in the average and worst case this is why, for larger datasets, more advanced algorithms like Merge Sort or Quick Sort (O(n log n)) are preferred. Bubble and Insertion Sort can perform much better (O(n)) specifically when the data is already sorted or nearly sorted.
