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

### Problem: Java's Built-in Sort
```java
import java.util.Arrays;

public class SortDemo {
    public static void main(String[] args) {
        int arr[] = {40, 10, 30, 20};
        Arrays.sort(arr);

        for (int num : arr) {
            System.out.println(num);
        }
    }
}
```
Java already has a built-in tool that can sort an array for you you don't have to write the logic yourself. You just hand your array over to Arrays.sort(arr), and it rearranges the numbers from smallest to largest, directly inside that same array. Then we just loop through and print the now-sorted values.

**Output:** 10, 20, 30, 40

This is what you'd actually use in a real project. But interviews and DSA learning expect you to understand how sorting works underneath which is what the rest of today covers.

### Problem: Bubble Sort
```java
public class BubbleSort {
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
        }

        System.out.println("Sorted array: " + java.util.Arrays.toString(arr));
    }
}
```
Imagine a row of people standing shoulder to shoulder by height, and you're walking down the row comparing each pair of neighbors. Whenever you find someone shorter standing after someone taller, you make them swap places. You keep walking down the row doing this by the time you reach the end, the tallest person has gradually "bubbled" all the way to the last position.
That's one full pass. Now you do it again but this time, since the tallest person is already correctly placed at the end, there's no need to include them in your walk anymore. Each pass, the walk gets one person shorter, because the end of the row is already sorted.
You repeat this process comparing neighbors, swapping when needed, shrinking your walk by one each time until the whole row is sorted, shortest to tallest.

**Why does the inner loop use n - i - 1?**
Because after each pass, one more element (the largest remaining one) has landed in its correct final spot at the end. There's no point re-checking something we already know is correctly placed.

### Problem: Bubble Sort (Optimized with Early Stop)
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
                break;
            }
        }

        System.out.println("Sorted array: " + java.util.Arrays.toString(arr));
    }
}
```
This is the exact same walk-down-the-row idea as regular Bubble Sort, but with one smart addition: we carry a little flag that starts as "false" (meaning "nothing has been swapped yet this round"). Every time we actually swap two people, we flip that flag to "true."
At the end of each full pass, we check the flag. If it's still "false" meaning we walked the entire row and didn't need to swap anyone that tells us the row is already completely sorted, and there's no point continuing. We stop immediately instead of doing more unnecessary passes.

**Why does this optimization matter?**
If the array is already sorted (or close to it), this saves a lot of wasted work instead of always doing every single pass no matter what, we quit early the moment we realize there's nothing left to fix.

### Problem: Bubble Sort — Display After Each Pass (Assignment)
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
This is identical to regular Bubble Sort same walk, same swapping logic except we added one extra line: right after finishing each full pass (each walk down the row), we print out what the array looks like at that exact moment. This lets you actually see the array slowly becoming more sorted, pass by pass, instead of only seeing the final result at the very end.

### Problem: Selection Sort (Ascending)
```java
public class SelectionSort {
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

            int temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
        }

        System.out.println("Sorted array (ascending): " + java.util.Arrays.toString(arr));
    }
}
```
Think of this like a teacher lining up students by height, one position at a time. For position 1 (the very front of the line), the teacher looks at every single student and finds whoever is shortest. That shortest student gets moved to position 1.
Now, for position 2, the teacher looks at everyone except the student already placed in position 1, finds the shortest among the remaining students, and moves them to position 2. This repeats for each position, scan everyone still unplaced, find the smallest, and put them there.
Notice this is different from Bubble Sort: here, we're not swapping neighbors repeatedly we scan the whole remaining group once per position, then do exactly one swap to put the right person in place.

**Output:** the array ends up as {11, 12, 22, 25, 64} — smallest to largest.

### Problem: Selection Sort (Descending)
```java
public class SelectionSortDescending {
    public static void main(String[] args) {
        int arr[] = {64, 25, 12, 22, 11};
        int n = arr.length;

        for (int i = 0; i < n - 1; i++) {
            int maxIndex = i;

            for (int j = i + 1; j < n; j++) {
                if (arr[j] > arr[maxIndex]) {
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
This is the exact same idea as regular Selection Sort, just flipped in one place: instead of hunting for the smallest remaining student each round, we hunt for the tallest one instead, and place them first. Every other part of the logic scanning the unplaced group, then doing one swap stays exactly the same.

###Problem: Selection Sort (Optimized — Skip Unnecessary Swaps)
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

            if (minIndex != i) {
                int temp = arr[minIndex];
                arr[minIndex] = arr[i];
                arr[i] = temp;
            }
        }

        System.out.println("Sorted array: " + java.util.Arrays.toString(arr));
    }
}
```
This works exactly like regular Selection Sort find the smallest remaining student, place them at the current position. The only difference: before actually doing the swap, we first ask "wait, is the smallest student already standing in this exact position?" If yes, swapping them with themselves would be pointless busywork, so we simply skip that step and move on to the next position.

### Problem: Insertion Sort
```java
public class InsertionSort {
    public static void main(String[] args) {
        int arr[] = {5, 2, 4, 6, 1, 3};
        int n = arr.length;

        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;

            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            arr[j + 1] = key;
        }

        System.out.println("Sorted array: " + java.util.Arrays.toString(arr));
    }
}
```
Picture sorting a hand of playing cards as you're dealt them, one at a time. Your first card is automatically "sorted" — there's nothing to compare it to yet. As you receive each new card, you hold it up (that's your key) and slide it leftward through your already-sorted cards, comparing it against each one, until you find the exact spot where it belongs — then you slot it in there. Every card to the right of that spot that was bigger than your new card gets nudged over to make room.
Let's trace through {5, 2, 4, 6, 1, 3}:

1. Start with 5 alone — that's our "sorted hand" so far
2. Pick up 2 — it's smaller than 5, so 5 slides right, and 2 goes in front → sorted so far: 2, 5
3. Pick up 4 — it's smaller than 5 but bigger than 2, so only 5 slides right → sorted so far: 2, 4, 5
4. Pick up 6 — it's bigger than everything already there, so nothing needs to move, it just stays at the end → 2, 4, 5, 6
5. Pick up 1 — it's smaller than everyone, so 2, 4, 5, and 6 all slide right to make room at the very front → 1, 2, 4, 5, 6
6. Pick up 3 — it slides past 6, 5, and 4 (all bigger), but stops before 2 (which is smaller) → 1, 2, 3, 4, 5, 6

**Output:** 1, 2, 3, 4, 5, 6

**Why start from index 1 instead of 0?**
A single card by itself is always technically "sorted" there's no one to compare it to. So we treat the very first element as our starting "sorted hand" of size one, and begin inserting from the second element onward.

### In short:
**1. Bubble Sort:** repeatedly compares and swaps neighbors, letting the biggest value gradually "bubble" to the end each pass
**2. Selection Sort:** scans the whole unsorted section to find the smallest (or biggest) value, and places it directly one swap per position
**3. Insertion Sort:** builds up a sorted section one element at a time, sliding each new element into its correct spot among what's already sorted
