# Day 08 — Stack, Queue, Deque & Applications

Topics:

1. Stack
2. Queue
3. Deque
4. Stack & Queue Applications

## 1. Stack

A Stack is a linear data structure that follows the LIFO principle Last In, First Out. The last element inserted is the first one removed, like a stack of plates: you add plates to the top, and you also remove from the top.

Core operations:

1. Push — insert an element onto the top
2. Pop — remove the element from the top
3. Peek — view the top element without removing it
4. isEmpty — check whether the stack is empty
5. isFull — check whether the stack is full (relevant for array-based stacks)

Stack Implementation Using an Array:
```java
public class StackArray {
    int stack[] = new int[5];
    int top = -1; // -1 means the stack is empty

    void push(int data) {
        if (top == stack.length - 1) {
            System.out.println("Stack Overflow");
        } else {
            stack[++top] = data; // increment top first, then insert
        }
    }

    void pop() {
        if (top == -1) {
            System.out.println("Stack Underflow");
        } else {
            top--; // simply move top back — the "removed" value is left behind but ignored
        }
    }

    void peek() {
        if (top == -1) {
            System.out.println("Stack is empty");
        } else {
            System.out.println("Top element: " + stack[top]);
        }
    }

    void display() {
        if (top == -1) {
            System.out.println("Stack is empty");
        } else {
            for (int i = top; i >= 0; i--) { // print from top down to bottom
                System.out.print(stack[i] + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        StackArray s = new StackArray();
        s.push(10);
        s.push(20);
        s.push(30);
        s.display();  // 30 20 10
        s.peek();      // Top element: 30
        s.pop();       // removes 30
        s.display();  // 20 10
    }
}
```
**Why stack[++top] = data (pre-increment) and not stack[top++] = data (post-increment)?**
We need to move top forward first, to point at the next empty slot, and then place the new value there. If we used post-increment, the value would get placed at the old position (overwriting the current top) before top moved which is incorrect.

Stack Implementation Using a Linked List:
```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class StackLinkedList {
    Node top;

    void push(int data) {
        Node newNode = new Node(data);
        newNode.next = top; // new node points to the old top
        top = newNode;       // new node becomes the new top
    }

    void pop() {
        if (top == null) {
            System.out.println("Stack Underflow");
        } else {
            System.out.println("Popped: " + top.data);
            top = top.next; // move top to the next node
        }
    }

    void peek() {
        if (top == null) {
            System.out.println("Stack is empty");
        } else {
            System.out.println("Top element: " + top.data);
        }
    }

    void display() {
        Node temp = top;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        StackLinkedList s = new StackLinkedList();
        s.push(10);
        s.push(20);
        s.push(30);
        s.display(); // 30 20 10
        s.pop();      // removes 30
        s.display(); // 20 10
    }
}
```
**Array vs Linked List implementation:** 
The array version has a fixed size (can overflow), while the linked list version can grow dynamically since new nodes are created as needed.
