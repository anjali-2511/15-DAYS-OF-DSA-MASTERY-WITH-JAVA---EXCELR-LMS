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

