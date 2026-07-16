# Day 03 — Advanced Arrays, Binary Search, Prefix Sum, Two Pointers, Sliding Window
Topics:

### 1. Advanced Arrays
### 2. Binary Search
### 3. Prefix Sum
### 4. Two Pointers Technique
### 5. Sliding Window Technique


## 1.  Advanced Arrays 

**Finding the Second Largest Element**
A common interview problem: given an array (which may contain duplicates), find the second largest distinct value.
```java
public class SecondLargest {
    public static void main(String[] args) {
        int arr[] = {10, 20, 4, 99, 99, 45};

        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;

        for (int num : arr) {
            if (num > largest) {
                secondLargest = largest; // old largest becomes second largest
                largest = num;           // new largest found
            } else if (num > secondLargest && num != largest) {
                secondLargest = num;     // update second largest, skip duplicates of largest
            }
        }

        if (secondLargest == Integer.MIN_VALUE) {
            System.out.println("No second largest element");
        } else {
            System.out.println("Second largest: " + secondLargest);
        }
    }
}
```
**Why Integer.MIN_VALUE?** 
It's simply Java's built-in constant for the smallest possible integer used here so that literally any number in the array will be bigger than our starting point, guaranteeing the first real comparison updates largest correctly.

**Why check num != largest in the second condition?** 
To correctly skip duplicate values of the largest number — e.g. in {10, 20, 4, 99, 99, 45}, the second 99 should not overwrite secondLargest, since it's a repeat of the largest value, not a genuinely different "second-highest" number.


## 2. Binary Search

Binary Search is a searching algorithm used to find an element in a sorted array. Instead of checking every element one by one (linear search), it repeatedly divides the search space in half, until the element is found or the search space becomes empty.

**Requirement:** the array must be sorted.

**Time complexity:** O(1) best case, O(log n) average/worst case
**Space complexity:** O(1) iterative, O(log n) recursive (due to the call stack)

**How it works:**
**Array:** {5, 10, 15, 20, 25, 30, 35} (indices 0–6), searching for 25:

1. low = 0, high = 6 → mid = 3 → arr[3] = 20. Since 25 > 20, search the right half
2. low = 4, high = 6 → mid = 5 → arr[5] = 30. Since 25 < 30, search the left half
3. low = 4, high = 4 → mid = 4 → arr[4] = 25. Match found!

**Code (Iterative):**
```java
public class BinarySearchDemo {
    public static void main(String[] args) {
        int arr[] = {5, 10, 15, 20, 25, 30, 35};
        int key = 25;
        int low = 0;
        int high = arr.length - 1;
        int foundIndex = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == key) {
                foundIndex = mid;
                break;
            } else if (key < arr[mid]) {
                high = mid - 1; // search left half
            } else {
                low = mid + 1;  // search right half
            }
        }

        if (foundIndex != -1) {
            System.out.println("Element found at index: " + foundIndex);
        } else {
            System.out.println("Element not found");
        }
    }
}
```
**Code (Recursive):**
```java
public class BinarySearchRecursive {
    public static void main(String[] args) {
        int arr[] = {2, 4, 6, 8, 10, 12, 14, 16};
        int key = 10;
        int index = binarySearch(arr, 0, arr.length - 1, key);

        if (index != -1) {
            System.out.println("Element found at index: " + index);
        } else {
            System.out.println("Element not found");
        }
    }

    public static int binarySearch(int arr[], int low, int high, int key) {
        if (low > high) {
            return -1; // base case: search space is empty
        }

        int mid = low + (high - low) / 2;

        if (arr[mid] == key) {
            return mid;
        } else if (key < arr[mid]) {
            return binarySearch(arr, low, mid - 1, key); // search left
        } else {
            return binarySearch(arr, mid + 1, high, key); // search right
        }
    }
}
```
**Why low + (high - low) / 2 instead of (low + high) / 2?**
Both give the same mathematical result, but low + (high - low) / 2 avoids a potential integer overflow issue when low and high are both very large numbers a good habit to build early.

## 3. Prefix Sum

**Prefix Sum** is a technique used to efficiently answer range sum queries 
i.e. **"what's the sum of elements from index X to index Y?"**
without repeatedly looping through the array each time.

Instead of recalculating the sum from scratch for every query (which takes O(n) time per query), we preprocess the array once into a prefix sum array, where each position stores the cumulative sum of all elements up to that point.

Code: 
```java
public class PrefixSumDemo {
    public static void main(String[] args) {
        int arr[] = {2, 4, 6, 8, 10, 12};
        int prefix[] = new int[arr.length];

        prefix[0] = arr[0]; // first value stays the same

        for (int i = 1; i < arr.length; i++) {
            prefix[i] = prefix[i - 1] + arr[i]; // add running total
        }

        System.out.println("Original array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }

        System.out.println("\nPrefix sum array:");
        for (int num : prefix) {
            System.out.print(num + " ");
        }
    }
}
```
**How the prefix array builds up:**
arr = {2, 4, 6, 8, 10, 12}
prefix[0] = 2
prefix[1] = 2 + 4 = 6
prefix[2] = 6 + 6 = 12
prefix[3] = 12 + 8 = 20
prefix[4] = 20 + 10 = 30
prefix[5] = 30 + 12 = 42

Once this is built, finding the sum of any range (e.g. index 2 to 5) becomes a quick subtraction (prefix[5] - prefix[1]) instead of looping through the whole range again.

## 4. Two Pointers Technique

The two-pointer technique uses two index pointers to traverse an array or string efficiently often replacing a nested loop (O(n²)) with a single pass (O(n)).

**Common setup:** one pointer starts from the beginning (left), one starts from the end (right), and they move toward each other based on a condition.

**Problem:** Find a pair with a given sum (in a sorted array)
```java
public class PairWithGivenSum {
    public static void main(String[] args) {
        int arr[] = {2, 4, 5, 7, 11, 15};
        int target = 15;

        int left = 0;
        int right = arr.length - 1;
        boolean found = false;

        while (left < right) {
            int sum = arr[left] + arr[right];

            if (sum == target) {
                System.out.println("Pair found: " + arr[left] + " + " + arr[right] + " = " + target);
                found = true;
                break;
            } else if (sum < target) {
                left++;  // sum too small, move left pointer forward to increase it
            } else {
                right--; // sum too big, move right pointer backward to decrease it
            }
        }

        if (!found) {
            System.out.println("Pair not found");
        }
    }
}
```
**How it converges on the answer (target = 15):**

1. arr[0] + arr[5] → 2 + 15 = 17 → too big → move right left
2. arr[0] + arr[4] → 2 + 11 = 13 → too small → move left right
3. arr[1] + arr[4] → 4 + 11 = 15 → match found!


## 5. Sliding Window Technique

The sliding window technique is an optimization used for problems involving contiguous subarrays or substrings. Instead of recalculating a result from scratch for every possible window, it reuses the previous window's result and just adjusts for what changed.

**There are two types:**

**1. Fixed-size window:** 
Window size stays constant (e.g. max sum of k consecutive elements)
**2. Variable-size window:**
Window size changes dynamically based on a condition (e.g. smallest subarray with a sum ≥ target)

**Fixed-size window:** Maximum sum of k consecutive elements
```java
public class SlidingWindowFixed {
    public static void main(String[] args) {
        int arr[] = {2, 1, 5, 1, 3, 2};
        int k = 3;

        int windowSum = 0;
        for (int i = 0; i < k; i++) {
            windowSum += arr[i]; // sum of the first window
        }

        int maxSum = windowSum;

        for (int i = k; i < arr.length; i++) {
            windowSum = windowSum - arr[i - k] + arr[i]; // slide: remove oldest, add newest
            maxSum = Math.max(maxSum, windowSum);
        }

        System.out.println("Maximum sum of " + k + " consecutive elements: " + maxSum);
    }
}
```
**How the window slides:**

1. First window (indices 0,1,2): 2 + 1 + 5 = 8
2. Slide right: remove arr[0]=2, add arr[3]=1 → 8 - 2 + 1 = 7
3. Slide right: remove arr[1]=1, add arr[4]=3 → 7 - 1 + 3 = 9
4. Slide right: remove arr[2]=5, add arr[5]=2 → 9 - 5 + 2 = 6
5. Maximum across all windows: 9

**Variable-size window:** Smallest subarray with a given sum
```java
public class SlidingWindowVariable {
    public static void main(String[] args) {
        int arr[] = {2, 1, 5, 2, 3, 2};
        int targetSum = 7;

        int windowSum = 0;
        int minLength = Integer.MAX_VALUE;
        int start = 0;

        for (int end = 0; end < arr.length; end++) {
            windowSum += arr[end]; // expand the window

            while (windowSum >= targetSum) {
                minLength = Math.min(minLength, end - start + 1);
                windowSum -= arr[start]; // shrink the window from the left
                start++;
            }
        }

        if (minLength == Integer.MAX_VALUE) {
            System.out.println("No subarray found with the given sum");
        } else {
            System.out.println("Smallest subarray length: " + minLength);
        }
    }
}
```
**Why this window is "variable":**
unlike the fixed-size version, the window grows (end moves forward, adding elements) and shrinks (start moves forward, removing elements) dynamically its size isn't fixed at k, it depends on whichever combination first satisfies the sum condition.


### Problem 1: Second Largest Element
```java
public class SecondLargest {
    public static void main(String[] args) {
        int arr[] = {10, 20, 4, 99, 99, 45};
        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;

        for (int num : arr) {
            if (num > largest) {
                secondLargest = largest;
                largest = num;
            } else if (num > secondLargest && num != largest) {
                secondLargest = num;
            }
        }

        if (secondLargest == Integer.MIN_VALUE) {
            System.out.println("No second largest element");
        } else {
            System.out.println("Second largest: " + secondLargest);
        }
    }
}
```
Imagine a "1st place" and "2nd place" podium, and both spots start out empty (represented by the smallest possible number Java can hold, so that literally any real number will beat it).
Now we walk through the array one number at a time. Every time we see a number, we ask: "Is this bigger than whoever is currently in 1st place?"

1. If yes — the old 1st place person gets bumped down to 2nd place, and this new number takes over 1st place.
2. If no — we ask a second question instead: "Is this bigger than whoever is in 2nd place, AND is it a genuinely different number from 1st place?" If both are true, this number takes over 2nd place.

Let's trace through {10, 20, 4, 99, 99, 45}:

1. 10 comes in → bigger than empty 1st place → 10 takes 1st, 2nd stays empty
2. 20 comes in → bigger than 10 → 20 takes 1st, 10 moves to 2nd
3. 4 comes in → not bigger than 20 (1st) → is it bigger than 10 (2nd)? No → nothing changes
4. 99 comes in → bigger than 20 → 99 takes 1st, 20 moves to 2nd
99 comes in again (duplicate) → is it bigger than 99 (current 1st)? No, they're equal → is it bigger than 20 (2nd) AND different from 1st place (99)? It's bigger than 20, but it's NOT different from 1st place (it IS 99) → so it's rejected, nothing changes
5. 45 comes in → not bigger than 99 → is it bigger than 20 (2nd) and different from 99? Yes to both → 45 takes over 2nd place

**Final:** 1st place = 99, 2nd place = 45.

**Output:** Second largest: 45

**Why check "different from 1st place"?**
Without that check, the duplicate 99 would have wrongly pushed itself into 2nd place too — but a repeated copy of the biggest number isn't really a "second, different, biggest" number. That check makes sure we only count genuinely different values.

### Problem 2: Binary Search (Iterative)
```java
public class BinarySearchDemo {
    public static void main(String[] args) {
        int arr[] = {5, 10, 15, 20, 25, 30, 35};
        int key = 25;
        int low = 0;
        int high = arr.length - 1;
        int foundIndex = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == key) {
                foundIndex = mid;
                break;
            } else if (key < arr[mid]) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        if (foundIndex != -1) {
            System.out.println("Element found at index: " + foundIndex);
        } else {
            System.out.println("Element not found");
        }
    }
}
```
Think of this like looking up a word in a paper dictionary. You don't start from page 1 and flip through one by one you open to roughly the middle, see if your word comes before or after that page, and then only search that half. You keep doing this, cutting your search area in half every time, until you find the word.
Here, low and high mark the boundaries of the section we're currently searching — at the start, that's the whole array. We keep looking as long as low hasn't crossed past high (meaning there's still something left to search).
Each round, we calculate the middle position (mid) of our current section and check the value sitting there:

1. If it matches what we're looking for (key) we're done, save that position and stop.
2. If our key is smaller than the middle value the answer must be somewhere in the left half, so we shrink our search area by moving high to just before the middle.
3. If our key is bigger the answer must be in the right half, so we move low to just after the middle.

Tracing through the array {5, 10, 15, 20, 25, 30, 35} looking for 25:

**1. First round:** middle of the whole array is index 3, which holds 20. Since 25 is bigger than 20, we now only search the right half.
**2. Second round:** middle of the right half is index 5, which holds 30. Since 25 is smaller than 30, we now only search the left part of that half.
**3. Third round:** only index 4 is left, which holds 25 — a match! We stop here.

**Output:** Element found at index: 4

**Why does this only work on a sorted array?**
The whole trick relies on being able to say "if my key is bigger than the middle value, it must be somewhere to the right." That's only guaranteed to be true if the numbers are arranged in order.


### Problem 3: Binary Search (Recursive)
```java
public class BinarySearchRecursive {
    public static void main(String[] args) {
        int arr[] = {2, 4, 6, 8, 10, 12, 14, 16};
        int key = 10;
        int index = binarySearch(arr, 0, arr.length - 1, key);

        if (index != -1) {
            System.out.println("Element found at index: " + index);
        } else {
            System.out.println("Element not found");
        }
    }

    public static int binarySearch(int arr[], int low, int high, int key) {
        if (low > high) {
            return -1;
        }

        int mid = low + (high - low) / 2;

        if (arr[mid] == key) {
            return mid;
        } else if (key < arr[mid]) {
            return binarySearch(arr, low, mid - 1, key);
        } else {
            return binarySearch(arr, mid + 1, high, key);
        }
    }
}
```
This does exactly the same job as Problem 2 — the only difference is how it repeats itself. Instead of using a loop that keeps updating low and high inside itself, this version has the function call itself with new, narrower boundaries each time. This is called recursion.
Every time we call binarySearch, we hand it a smaller slice of the array to search (by passing in a new low or high). Eventually, one of two things happens: either we find the middle value matches our key (and we return its position), or our search range becomes invalid (low crosses past high, meaning there's nothing left to check) — this second case is called the base case, and it's what stops the recursion from calling itself forever.

**Output:** Element found at index: 4

**Why does recursion need a base case?**
Without a stopping condition (if (low > high) return -1;), the function would keep calling itself endlessly, since there'd be nothing to tell it "stop, you're done." The base case is what breaks the chain.

### Problem 4: Prefix Sum
```java
public class PrefixSumDemo {
    public static void main(String[] args) {
        int arr[] = {2, 4, 6, 8, 10, 12};
        int prefix[] = new int[arr.length];

        prefix[0] = arr[0];

        for (int i = 1; i < arr.length; i++) {
            prefix[i] = prefix[i - 1] + arr[i];
        }

        System.out.println("Original array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }

        System.out.println("\nPrefix sum array:");
        for (int num : prefix) {
            System.out.print(num + " ");
        }
    }
}
```
Imagine you're keeping a running total of your bank balance after every deposit — not just knowing today's deposit, but knowing your total balance so far after each one. That's exactly what a prefix sum array does.
We create a new array (prefix) the same size as our original one. The very first spot just copies whatever the original array's first value is — nothing to add yet. From the second spot onward, each position takes the previous running total and adds the current original value to it.
Tracing through {2, 4, 6, 8, 10, 12}:

1. First spot: just copy 2 → running total so far: 2
2. Second spot: previous total (2) + current value (4) = 6
3. Third spot: previous total (6) + current value (6) = 12
4. Fourth spot: previous total (12) + current value (8) = 20
5. Fifth spot: previous total (20) + current value (10) = 30
6. Sixth spot: previous total (30) + current value (12) = 42

**Output:**
Original array: 2 4 6 8 10 12
Prefix sum array: 2 6 12 20 30 42

**Why bother building this extra array?**
Once it's built, if someone asks "what's the total of elements from position 2 to position 5?", instead of adding those numbers one by one every single time someone asks, you can just subtract two values from the prefix array instant answer, no matter how many times the question gets asked.

### Problem 5: Two Pointers — Pair With Given Sum
```java
public class PairWithGivenSum {
    public static void main(String[] args) {
        int arr[] = {2, 4, 5, 7, 11, 15};
        int target = 15;

        int left = 0;
        int right = arr.length - 1;
        boolean found = false;

        while (left < right) {
            int sum = arr[left] + arr[right];

            if (sum == target) {
                System.out.println("Pair found: " + arr[left] + " + " + arr[right] + " = " + target);
                found = true;
                break;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }

        if (!found) {
            System.out.println("Pair not found");
        }
    }
}
```
Imagine standing at two ends of a sorted line of numbers — one hand pointing at the very first (smallest) number, the other hand pointing at the very last (biggest) number. We want to find two numbers that add up exactly to our target.
We add the two numbers our hands are pointing at. Three things can happen:

1. If they add up to exactly our target — we found our pair, done!
2. If the sum is too small — we need a bigger number, so we move our "left hand" one step to the right (toward bigger numbers).
3. If the sum is too big — we need a smaller number, so we move our "right hand" one step to the left (toward smaller numbers).

We keep doing this, and our two hands gradually move toward each other, until either they meet in the middle or we find a match.

Tracing through {2, 4, 5, 7, 11, 15} looking for a pair that sums to 15:
1. Left points to 2, right points to 15 → sum is 17, too big → move right hand inward
2. Left points to 2, right points to 11 → sum is 13, too small → move left hand inward
3. Left points to 4, right points to 11 → sum is 15 → match found!

**Output:** Pair found: 4 + 11 = 15

**Why does this only work on a sorted array?**
Moving the left pointer forward only makes sense as "get a bigger number" if the array is arranged from smallest to biggest. On an unsorted array, we couldn't reliably predict whether shifting a pointer would increase or decrease the sum.

### Problem 6: Sliding Window (Fixed Size) — Max Sum of K Consecutive Elements
```java
public class SlidingWindowFixed {
    public static void main(String[] args) {
        int arr[] = {2, 1, 5, 1, 3, 2};
        int k = 3;

        int windowSum = 0;
        for (int i = 0; i < k; i++) {
            windowSum += arr[i];
        }

        int maxSum = windowSum;

        for (int i = k; i < arr.length; i++) {
            windowSum = windowSum - arr[i - k] + arr[i];
            maxSum = Math.max(maxSum, windowSum);
        }

        System.out.println("Maximum sum of " + k + " consecutive elements: " + maxSum);
    }
}
```
Imagine holding a physical picture frame that can only show 3 numbers at a time, and you're sliding it across a row of numbers, one step at a time, trying to find where the 3 numbers inside the frame add up to the most.
Instead of re-adding all 3 numbers every time you slide the frame over (which would be wasteful), there's a shortcut: when the frame slides one step to the right, you only need to remove the number that just left the frame and add the new number that just entered it — everything else inside the frame stayed the same, so there's no need to recalculate it from scratch.
First, we calculate the sum of the very first frame position (the first 3 numbers): 2 + 1 + 5 = 8. We save this as our best sum so far (maxSum).
Then we start sliding:

1. Slide once: remove the number that left (2), add the number that entered (1) → new sum = 8 − 2 + 1 = 7. Not better than 8, so maxSum stays 8.
2. Slide again: remove 1, add 3 → new sum = 7 − 1 + 3 = 9. That's better! maxSum updates to 9.
3. Slide again: remove 5, add 2 → new sum = 9 − 5 + 2 = 6. Not better, maxSum stays 9.

**Output:** Maximum sum of 3 consecutive elements: 9

**Why is this faster than recalculating each window from scratch?**
Recalculating all 3 numbers every time you slide means repeating work you already did. By just swapping out the one number that left for the one that entered, you do a tiny, constant amount of work per slide instead of redoing the whole sum — much faster on large arrays.

### Problem 7: Bonus: Sliding Window (Variable Size) — Smallest Subarray With a Given Sum
```java
public class SlidingWindowFixed {
    public static void main(String[] args) {
        int arr[] = {2, 1, 5, 1, 3, 2};
        int k = 3;

        int windowSum = 0;
        for (int i = 0; i < k; i++) {
            windowSum += arr[i];
        }

        int maxSum = windowSum;

        for (int i = k; i < arr.length; i++) {
            windowSum = windowSum - arr[i - k] + arr[i];
            maxSum = Math.max(maxSum, windowSum);
        }

        System.out.println("Maximum sum of " + k + " consecutive elements: " + maxSum);
    }
}
```
This time, our "picture frame" isn't a fixed size — it can stretch wider or shrink narrower depending on what we need. Our goal: find the smallest possible stretch of consecutive numbers that adds up to at least our target sum (7).
We have two edges of our frame: start (left edge) and end (right edge). We keep pushing the right edge (end) forward, adding each new number to our running total (windowSum) this is the frame "growing."
But as soon as our running total reaches or passes the target, we try shrinking from the left (start) as much as possible while still keeping the total at or above the target because a smaller frame that still meets the goal is exactly what we're looking for. Each time we successfully shrink, we check if this is the smallest frame we've seen so far, and remember it.
Once shrinking would drop us below the target, we stop shrinking, go back to growing from the right, and repeat the whole process.

**Output:** Smallest subarray length: 2 (the numbers 5 and 2 add up to exactly 7)

**Why does the frame need to both grow AND shrink?**
Growing (moving end forward) is how we search for any combination that reaches the target. Shrinking (moving start forward) is how we make sure we've found the smallest combination, not just the first one that happened to work.
