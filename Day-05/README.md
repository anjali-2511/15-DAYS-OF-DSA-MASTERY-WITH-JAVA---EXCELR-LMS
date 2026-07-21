# Day 05 — Strings, Character Arrays, StringBuilder & String Manipulation

Topics:
1. Strings
2. Character Arrays
3. StringBuilder
4. String Manipulation Problems

## 1. Strings

A string is a sequence of characters enclosed within double quotes. In Java, a string is an object of the String class, and it is immutable once created, its value cannot be changed. 
If you try to "change" a string, Java actually creates a new object behind the scenes rather than modifying the original.

**Why are strings important in DSA?**
They're one of the most frequently used data structures in coding interviews used for text processing, pattern matching, password validation, search engines, DNA sequence analysis, chat applications, compiler design, and NLP (Natural Language Processing).

**Memory representation:** Just like an array, each character in a string has an index starting from 0. For example, in "Java": J is at index 0, a at index 1, v at index 2, a at index 3.

Two ways to create a String in Java
```java
String name1 = "Java";              // string literal
String name2 = new String("Java");  // using the new keyword
```

Common String methods
```java
public class StringExample {
    public static void main(String[] args) {
        String name = "Java";

        System.out.println(name);                     // Java
        System.out.println(name.length());             // 4
        System.out.println(name.toUpperCase());        // JAVA
        System.out.println(name.toLowerCase());        // java
        System.out.println(name.charAt(0));             // J

        String text = "  Hello World  ";
        System.out.println(text.substring(0, 5));       // Hello (part of the string)
        System.out.println(text.trim());                 // "Hello World" (removes leading/trailing spaces)
        System.out.println(text.contains("World"));      // true
        System.out.println(text.replace("World", "Java"));// replaces characters
        System.out.println(text.equalsIgnoreCase("  hello world  ")); // true — ignores case

        String csv = "a,b,c,d";
        String[] parts = csv.split(",");                // splits the string into an array

        System.out.println(csv.indexOf("b"));            // first occurrence position
        System.out.println(csv.lastIndexOf("b"));         // last occurrence position
    }
}
```

Quick reference of methods covered:
| Method | Purpose |
|--------|---------|
| `length()` | returns the string's length |
| `charAt(index)` | returns the character at a position |
| `substring(start, end)` | returns part of the string |
| `toUpperCase()` / `toLowerCase()` | case conversion |
| `equals()` / `equalsIgnoreCase()` | compares two strings (with/without case sensitivity) |
| `contains()` | checks if a substring exists |
| `replace()` | replaces characters/substrings |
| `trim()` | removes leading/trailing spaces |
| `split()` | splits a string into an array |
| `indexOf()` / `lastIndexOf()` | finds first/last occurrence of a character |


## 2. String Manipulation Problems (using String)

### Problem: Reverse a String
```java
public class ReverseString {
    public static void main(String[] args) {
        String str = "hello";
        String reverse = "";

        for (int i = str.length() - 1; i >= 0; i--) {
            reverse = reverse + str.charAt(i);
        }

        System.out.println("Original: " + str);
        System.out.println("Reversed: " + reverse);
    }
}
```

### Problem: Check if a String is a Palindrome
(A palindrome reads the same forwards and backwards — e.g. "madam")
```java
public class CheckPalindrome {
    public static void main(String[] args) {
        String str = "madam";
        int left = 0;
        int right = str.length() - 1;
        boolean isPalindrome = true;

        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                isPalindrome = false;
                break;
            }
            left++;
            right--;
        }

        if (isPalindrome) {
            System.out.println(str + " is a palindrome");
        } else {
            System.out.println(str + " is not a palindrome");
        }
    }
}
```

### Problem: Count Vowels and Consonants
```java
public class CountVowelsConsonants {
    public static void main(String[] args) {
        String str = "programming";
        str = str.toLowerCase();
        int vowels = 0, consonants = 0;

        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);

            if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
                vowels++;
            } else if (Character.isLetter(ch)) {
                consonants++;
            }
        }

        System.out.println("Vowels: " + vowels);
        System.out.println("Consonants: " + consonants);
    }
}
```
**Why check Character.isLetter(ch)?**
This makes sure we only count actual alphabet characters as consonants skipping spaces, numbers, or punctuation that might be in the string.


## 3. Character Arrays

A character array stores individual characters, where each element is of type char. Unlike String, a character array is mutable you can change individual characters directly, without creating a new object each time.

String vs Character Array:

| Aspect | String | Character Array |
|--------|--------|------------------|
| Mutability | Immutable | Mutable |
| Type | Object of String class | Primitive array |
| Built-in methods | Rich set of methods | Manual processing needed |
| Modifying characters | Cannot modify directly | Can modify directly |
| Common use | General text handling | DSA algorithms, in-place manipulation |

### Creating and printing a character array
```java
public class CharArrayDemo {
    public static void main(String[] args) {
        char arr[] = {'j', 'a', 'v', 'a'};

        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```

### Reversing a Character Array (in-place, using two pointers)
```java
public class ReverseCharArray {
    public static void main(String[] args) {
        char arr[] = {'h', 'e', 'l', 'l', 'o'};
        int left = 0;
        int right = arr.length - 1;

        while (left < right) {
            char temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }

        System.out.println("Reversed: " + new String(arr));
    }
}
```

### Count Vowels and Consonants (using Character Array)
```java
public class CountVowelsCharArray {
    public static void main(String[] args) {
        char arr[] = {'p', 'r', 'o', 'g', 'r', 'a', 'm'};
        int vowels = 0, consonants = 0;

        for (char ch : arr) {
            ch = Character.toLowerCase(ch);
            if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
                vowels++;
            } else {
                consonants++;
            }
        }

        System.out.println("Vowels: " + vowels);
        System.out.println("Consonants: " + consonants);
    }
}
```

## 4. StringBuilder

StringBuilder is a mutable class in Java used to create and modify strings efficiently. Unlike String (which is immutable), a StringBuilder object can be changed without creating a new object every time. It belongs to the java.lang package.

**Why use StringBuilder?**
If you need to concatenate strings repeatedly (e.g. inside a loop), using regular String creates a brand-new object every single time wasteful and slow. StringBuilder reuses the same object instead, making repeated modifications much faster.

String vs StringBuilder:

| Aspect | String | StringBuilder |
|--------|--------|----------------|
| Mutability | No (immutable) | Yes (mutable) |
| Thread safety | Not thread-safe | Not thread-safe |
| Performance for modification | Slower — creates new object each time | Faster — reuses same object |
| Best suited for | Fixed text | Frequently changing text |

### Creating a StringBuilder and appending
```java
public class StringBuilderDemo {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");

        sb.append(" Programming"); // adds text using the same object

        System.out.println(sb);
    }
}
```
### Common StringBuilder methods
```java
public class StringBuilderMethods {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello World");

        sb.append("!");                    // adds text at the end
        System.out.println(sb);            // Hello World!

        sb.insert(5, ",");                  // inserts text at a specific position
        System.out.println(sb);            // Hello, World!

        sb.delete(5, 6);                    // deletes characters in a range
        System.out.println(sb);            // Hello World!

        sb.replace(0, 5, "Hi");             // replaces characters in a range
        System.out.println(sb);            // Hi World!

        sb.reverse();                        // reverses the entire string
        System.out.println(sb);

        sb.setCharAt(0, 'X');               // changes a single character
        System.out.println(sb.length());    // returns current length
        System.out.println(sb.capacity());  // returns current capacity
        System.out.println(sb.toString());  // converts back to a String
    }
}
```
Difference between replace() and setCharAt(): replace() can swap out multiple characters within a range, while setCharAt() changes only one single character at a specific index.

## 5. More String Manipulation Problems

### Problem: Count Frequency of Each Character (using HashMap)
```java
import java.util.HashMap;

public class CountCharacterFrequency {
    public static void main(String[] args) {
        String str = "banana";
        HashMap<Character, Integer> map = new HashMap<>();

        for (char ch : str.toCharArray()) {
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }

        System.out.println(map);
    }
}
```
**How this works:** map.getOrDefault(ch, 0) checks if this character has already been seen before. If yes, it returns the current count; if not, it returns 0 (the default). Either way, we add 1 to that value and store it back — building up a running count for every character in the string.

### Problem: Remove Duplicate Characters
(Given as a self-practice assignment at the end of the session here's a working solution)
```java
public class RemoveDuplicateCharacters {
    public static void main(String[] args) {
        String str = "programming";
        StringBuilder result = new StringBuilder();

        for (char ch : str.toCharArray()) {
            if (result.indexOf(String.valueOf(ch)) == -1) { // character not already added
                result.append(ch);
            }
        }

        System.out.println("After removing duplicates: " + result);
    }
}
```
**How this works:** We build up our result one character at a time, but before adding each character, we check whether it's already present in our result so far (indexOf returns -1 if not found). Only genuinely new characters get appended — duplicates are silently skipped.

**Key Poits:**
1. A String is immutable — any "modification" actually creates a new object behind the scenes
2. Character arrays are mutable, making them useful for in-place string manipulation (like reversing)
3. StringBuilder is the efficient choice when you need to repeatedly modify or build up a string it avoids creating a new object on every change
4. Two-pointer logic applies directly to string/character-array problems reversing, palindrome checking
5. HashMap is a natural fit for counting-based string problems (like character frequency)


### 1. Problem: Reverse a String
```java
public class ReverseString {
    public static void main(String[] args) {
        String str = "hello";
        String reverse = "";

        for (int i = str.length() - 1; i >= 0; i--) {
            reverse = reverse + str.charAt(i);
        }

        System.out.println("Original: " + str);
        System.out.println("Reversed: " + reverse);
    }
}
```
We start with an empty "reverse" bucket nothing in it yet. Then, instead of walking through our word from the beginning, we start from the last letter and walk backward toward the first.
Each letter we visit gets added onto the end of our reverse bucket. So the very last letter of the original word becomes the very first letter we add which means it naturally ends up building the word backward.
Tracing through "hello":

1. Start at the last letter, o → bucket: "o"
2. Next letter back, l → bucket: "ol"
3. Next, l → bucket: "oll"
4. Next, e → bucket: "olle"
5. Next, h → bucket: "olleh"

**Output:** Reversed: olleh

### 2. Problem: Check if a String is a Palindrome
```java
public class CheckPalindrome {
    public static void main(String[] args) {
        String str = "madam";
        int left = 0;
        int right = str.length() - 1;
        boolean isPalindrome = true;

        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) {
                isPalindrome = false;
                break;
            }
            left++;
            right--;
        }

        if (isPalindrome) {
            System.out.println(str + " is a palindrome");
        } else {
            System.out.println(str + " is not a palindrome");
        }
    }
}
```
A palindrome is a word that reads exactly the same forward and backward like "madam" or "level." To check this, we don't need to fully reverse the word; we just need to compare it against itself from both ends, moving inward.
We place one pointer (left) at the very first letter, and another pointer (right) at the very last letter. We compare the letters they're pointing at — if they don't match, we immediately know it's not a palindrome, and we stop right there. If they do match, we move both pointers one step closer to the middle (left moves forward, right moves backward) and compare again.
We keep doing this until the two pointers meet in the middle. If we never found a mismatch along the way, the word is a palindrome.
Tracing through "madam":

1. left at m (position 0), right at m (position 4) → they match → move inward
2. left at a (position 1), right at a (position 3) → they match → move inward
3. left and right now meet at the middle (d) → loop stops, no mismatches found

**Output:** madam is a palindrome

### 3. Problem: Count Vowels and Consonants
```java
public class CountVowelsConsonants {
    public static void main(String[] args) {
        String str = "programming";
        str = str.toLowerCase();
        int vowels = 0, consonants = 0;

        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);

            if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
                vowels++;
            } else if (Character.isLetter(ch)) {
                consonants++;
            }
        }

        System.out.println("Vowels: " + vowels);
        System.out.println("Consonants: " + consonants);
    }
}
```
First, we convert the whole word to lowercase this way we don't have to separately check for both 'A' and 'a', we just handle one case.
Then we walk through the word letter by letter. For each letter, we ask: "Is this one of the 5 vowels (a, e, i, o, u)?" If yes, we add one to our vowel counter. If no, we ask a second question: "Is this at least a real letter (not a space, number, or symbol)?" If yes, it must be a consonant, so we add one to that counter instead.
By the end, we know exactly how many vowels and how many consonants were in the word.

**Output:** for "programming" — Vowels: 3, Consonants: 8

### 4. Problem: Character Array Basics
```java
public class CharArrayDemo {
    public static void main(String[] args) {
        char arr[] = {'j', 'a', 'v', 'a'};

        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```
Instead of storing the word "java" as one single String object, we store it as separate individual letter boxes a character array, where each box holds exactly one letter. We then loop through and print each box one at a time. This is the same basic array-traversal idea from Day 2, just applied to letters instead of numbers.

### 5. problem: Reversing a Character Array (In-Place)
```java
public class ReverseCharArray {
    public static void main(String[] args) {
        char arr[] = {'h', 'e', 'l', 'l', 'o'};
        int left = 0;
        int right = arr.length - 1;

        while (left < right) {
            char temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }

        System.out.println("Reversed: " + new String(arr));
    }
}
```
This is the two-pointer swapping trick again same idea as the palindrome check, but this time we're actually swapping instead of just comparing. One pointer starts at the first letter, another starts at the last letter. We swap whatever they're pointing at, then move both pointers one step closer to the middle, and repeat.
Because a character array is mutable (unlike a String), we can directly swap letters inside the same array — no need to build a brand-new word letter by letter like we did with the String version of reverse.
Tracing through {'h','e','l','l','o'}:

1. Swap position 0 (h) and position 4 (o) → array becomes o,e,l,l,h
2. Move inward: swap position 1 (e) and position 3 (l) → array becomes o,l,l,e,h
3. Pointers meet in the middle → done

**Output:** Reversed: olleh

### 6. Problem: StringBuilder — Append and Common Methods

```java
public class StringBuilderDemo {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" Programming");
        System.out.println(sb);
    }
}
```
Think of a StringBuilder like a notepad you can keep writing on, versus a String, which is like a printed page you'd have to reprint entirely every time you wanted to add a word. With append(), we just keep adding text onto the same notepad no new object gets created behind the scenes each time, which makes repeated changes much faster than doing the same thing with regular Strings.

**Output:** Hello Programming

The other StringBuilder methods work similarly all modifying the same object directly:

1. insert(position, text) — squeezes new text in at a specific spot, shifting everything after it to make room
2. delete(start, end) — removes a chunk of characters between two positions
3. replace(start, end, newText) — swaps out a chunk of characters for something new
4. reverse() — flips the entire content backward
5. setCharAt(position, newChar) — changes just one single character at a specific spot (unlike replace(), which can change multiple characters at once)

### 7. Problem: Count Frequency of Each Character (Using HashMap)
```java
import java.util.HashMap;

public class CountCharacterFrequency {
    public static void main(String[] args) {
        String str = "banana";
        HashMap<Character, Integer> map = new HashMap<>();

        for (char ch : str.toCharArray()) {
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }

        System.out.println(map);
    }
}
```
Think of a HashMap like a set of labeled boxes, one for each unique letter, where each box holds a running count of how many times that letter has appeared.
We go through the word one letter at a time. For each letter, we ask the map: "Have you seen this letter before?" If yes, getOrDefault hands us back the current count for that letter; if no, it hands us 0 since there's no box for it yet. Either way, we add 1 to whatever we got back, and store that new number back into the map under that letter.
Tracing through "banana":

1. b → not seen before → 0 + 1 = 1 → map: {b=1}
2. a → not seen before → 0 + 1 = 1 → map: {b=1, a=1}
3. n → not seen before → 0 + 1 = 1 → map: {b=1, a=1, n=1}
4. a → seen once already → 1 + 1 = 2 → map: {b=1, a=2, n=1}
5. n → seen once already → 1 + 1 = 2 → map: {b=1, a=2, n=2}
6. a → seen twice already → 2 + 1 = 3 → map: {b=1, a=3, n=2}

**Output:** {a=3, b=1, n=2} (order in the printed map may vary)

### 8. Problem: Remove Duplicate Characters (Assignment)
```java
public class RemoveDuplicateCharacters {
    public static void main(String[] args) {
        String str = "programming";
        StringBuilder result = new StringBuilder();

        for (char ch : str.toCharArray()) {
            if (result.indexOf(String.valueOf(ch)) == -1) {
                result.append(ch);
            }
        }

        System.out.println("After removing duplicates: " + result);
    }
}
```
We build up our answer one letter at a time inside a StringBuilder, but before adding any letter, we first check: "Have I already added this exact letter to my result?" We do this by searching for it inside what we've built so far if indexOf can't find it (returns -1), that means it's genuinely new, so we add it. If it's already there, we simply skip it and move to the next letter.
Tracing through "programming":

1. p → not in result yet → add it → result: "p"
2. r → not in result → add → result: "pr"
3. o → not in result → add → result: "pro"
4. g → not in result → add → result: "prog"
5. r → already in result → skip
6. a → not in result → add → result: "proga"
7. m → not in result → add → result: "progam"
8. m → already in result → skip
9. i → not in result → add → result: "progami"
10. n → not in result → add → result: "programin"
11. g → already in result → skip

**Output:** After removing duplicates: programin

### Short Note: 

1. String is great for general text handling but is immutable — every change makes a new object
2. Character array gives you direct, in-place control over individual letters perfect for reversing or manipulating text efficiently
3. StringBuilder is the best choice when you're repeatedly building or modifying text, since it avoids the overhead String would create
4. Many string problems reuse the same two-pointer pattern from reverse, palindrome check recognizing that pattern makes these problems much faster to solve
5. HashMap is a natural tool whenever you need to count or track occurrences of something here, individual characters
