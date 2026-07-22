# Day 07 — Linked List: Singly, Doubly & Circular

Topics:

1. Linked List
2. Singly Linked List
3. Doubly Linked List
4. Circular Linked List

## 1. Linked List

**What is a Linked List?**
A Linked List is a linear data structure in which elements (called nodes) are connected using pointers/references, instead of being stored in contiguous memory locations like an array.

Each node has two parts:
1. Data — the actual value stored
2. Next — a reference (address) pointing to the next node in the list

Unlike arrays, a linked list doesn't need a fixed size upfront, and inserting/removing elements doesn't require shifting other elements around in memory.

### Types of Linked List:

## 2. Singly Linked List

A Singly Linked List is the simplest type of linked list. Each node contains data and a reference to the next node. The last node's next reference points to null, marking the end of the list allowing traversal in only one direction (forward).

**Analogy:** Think of a train an engine followed by coach 1, coach 2, coach 3. Each coach only knows about the coach directly after it, not the one before. You can only move forward through the train, one coach at a time.

**Memory representation:** data | next → data | next → data | next → null

Creating a Node in Java:
```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```
**Why this.data = data?**
This refers to the current object's variable, distinguishing it from the data parameter passed into the constructor without this, Java wouldn't know whether you mean the class's variable or the parameter.

Basic example: creating and linking nodes manually:
```java
public class SinglyLinkedListDemo {
    public static void main(String[] args) {
        Node first = new Node(10);
        Node second = new Node(20);
        Node third = new Node(30);

        // manually connecting the nodes
        first.next = second;
        second.next = third;

        // displaying the list
        Node temp = first;
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }
}
```
**Output:** 10 -> 20 -> 30 -> null

Full implementation with reusable insert() and display() methods:
```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class SinglyLinkedList {
    Node head;

    void insert(int data) {
        Node newNode = new Node(data);

        if (head == null) {
            head = newNode; // list was empty, new node becomes the head
        } else {
            Node temp = head;
            while (temp.next != null) {
                temp = temp.next; // walk to the last node
            }
            temp.next = newNode; // attach new node at the end
        }
    }

    void display() {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        SinglyLinkedList list = new SinglyLinkedList();
        list.insert(10);
        list.insert(20);
        list.insert(30);
        list.display();
    }
}
```
**Output:** 10 -> 20 -> 30 -> null

**Why check if (head == null) before inserting?**
If the list is empty, there's no existing chain to walk through the new node simply becomes the starting point (head). If the list already has nodes, we need to walk all the way to the last node (while (temp.next != null)) before attaching the new one.
