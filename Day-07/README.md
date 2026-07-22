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

## 3. Doubly Linked List

A Doubly Linked List is similar to a singly linked list, but each node stores two references one to the previous node and one to the next node in addition to its data. This allows traversal in both directions: forward and backward.

**Analogy:** A music playlist you can see the previous song, current song, and next song. You can skip forward or go back, unlike a one-way train.

**Memory representation:** previous ← data → next, chained together in both directions.

Creating a Doubly Linked List Node:
```java
class DNode {
    int data;
    DNode prev;
    DNode next;

    DNode(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}
```
Full implementation: insert at end, display forward, display backward:
```java
public class DoublyLinkedList {
    DNode head;

    void insert(int data) {
        DNode newNode = new DNode(data);

        if (head == null) {
            head = newNode;
        } else {
            DNode temp = head;
            while (temp.next != null) {
                temp = temp.next; // walk to the last node
            }
            temp.next = newNode;    // link forward
            newNode.prev = temp;    // link backward
        }
    }

    void displayForward() {
        DNode temp = head;
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }

    void displayBackward() {
        if (head == null) return;

        DNode temp = head;
        while (temp.next != null) {
            temp = temp.next; // walk to the last node first
        }

        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.prev; // then walk backward
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        DoublyLinkedList list = new DoublyLinkedList();
        list.insert(10);
        list.insert(20);
        list.insert(30);

        System.out.println("Forward:");
        list.displayForward();

        System.out.println("Backward:");
        list.displayBackward();
    }
}
```
Output:
```
Forward:
10 -> 20 -> 30 -> null
Backward:
30 -> 20 -> 10 -> null
```
Inserting at the beginning:
```java
void insertAtBeginning(int data) {
    DNode newNode = new DNode(data);

    if (head == null) {
        head = newNode;
    } else {
        newNode.next = head;   // new node points forward to the old head
        head.prev = newNode;   // old head points backward to the new node
        head = newNode;        // new node becomes the new head
    }
}
```
Singly Linked List vs Doubly Linked List:

| Aspect | Singly Linked List | Doubly Linked List |
|--------|---------------------|----------------------|
| Traversal direction | Forward only | Forward and backward |
| References per node | 1 (`next`) | 2 (`prev` and `next`) |
| Memory usage | Lower | Higher (extra reference per node) |
| Use case | Simple one-directional lists | Playlists, browser history, undo/redo |
