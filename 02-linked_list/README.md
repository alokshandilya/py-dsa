# Linked List

- data structure that consists of a sequence of elements, each element links to the next element in the sequence.
- each element in a linked list is called a node. Each node has two components:
  - data: holds the value of the node
  - next: points to the next node in the sequence

In Python, we can implement a linked list using a class. Each node in the linked list is an object of the class. The class has two attributes: data and next. The data attribute holds the value of the node and the next attribute points to the next node in the sequence.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
```

## Singly Linked List

- a linked list in which each node points to the next node in the sequence.
- the last node in the sequence points to None.

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

# Implementation for Singly Linked List
class LinkedList:
    def __init__(self):
        # Init the list with a 'dummy' node which makes
        # removing a node from the beginning of list easier.
        self.head = ListNode(-1)
        self.tail = self.head

    def insertEnd(self, val):
        self.tail.next = ListNode(val)
        self.tail = self.tail.next

    def remove(self, index):
        i = 0
        curr = self.head
        while i < index and curr:
            i += 1
            curr = curr.next

        # Remove the node ahead of curr
        if curr:
            curr.next = curr.next.next

    def print(self):
        curr = self.head.next
        while curr:
            print(curr.val, ' -> ')
            curr = curr.next
        print()
```
