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
