# Design Linked List

**Difficulty:** Medium

**Topic:** Linked List, Design

**LeetCode Link: (707)** [Design Linked List](https://leetcode.com/problems/design-linked-list/)

Design your implementation of the linked list. You can choose to use a singly or doubly linked list.

A node in a singly linked list should have two attributes: `val` and `next`. `val` is the value of the current node, and `next` is a pointer/reference to the next node.

If you want to use the doubly linked list, you will need one more attribute `prev` to indicate the previous node in the linked list. Assume all nodes in the linked list are **0-indexed**.

Implement the `MyLinkedList` class:

- `MyLinkedList()` Initializes the `MyLinkedList` object.
- `int get(int index)` Get the value of the `index`-th node in the linked list. If the index is invalid, return `-1`.
- `void addAtHead(int val)` Add a node of value `val` before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
- `void addAtTail(int val)` Append a node of value `val` as the last element of the linked list.
- `void addAtIndex(int index, int val)` Add a node of value `val` before the `index`-th node in the linked list. If `index` equals the length of the linked list, the node will be appended to the end. If `index` is greater than the length, the node **will not be inserted**.
- `void deleteAtIndex(int index)` Delete the `index`-th node in the linked list, if the index is valid.

### Example 1:

```
Input:
["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"]
[[], [1], [3], [1, 2], [1], [1], [1]]
Output:
[null, null, null, null, 2, null, 3]

Explanation:
MyLinkedList myLinkedList = new MyLinkedList();
myLinkedList.addAtHead(1);
myLinkedList.addAtTail(3);
myLinkedList.addAtIndex(1, 2);    // linked list becomes 1->2->3
myLinkedList.get(1);              // return 2
myLinkedList.deleteAtIndex(1);    // now the linked list is 1->3
myLinkedList.get(1);              // return 3
```

#### Constraints:

- `0 <= index, val <= 1000`
- Please do not use the built-in LinkedList library.
- At most `2000` calls will be made to `get`, `addAtHead`, `addAtTail`, `addAtIndex`, and `deleteAtIndex`.

## Approach 1: Doubly Linked List ✅

```python
class ListNode:
    # each element in the doubly linked list
    def __init__(self, val):
        self.val = val  # value of the node
        self.prev = None  # pointer to the previous node
        self.next = None  # pointer to the next node

class MyLinkedList:
    def __init__(self):
        # 2 dummy nodes (left, right) as placeholders
        # this avoids dealing with null pointers performing insertion/deletion at head/tail
        self.left = ListNode(0)
        self.right = ListNode(0)

        # connect left and right dummy nodes
        self.left.next = self.right
        self.right.prev = self.left


    def get(self, index: int) -> int:
        # start at first real node
        curr = self.left.next

        # traverse the list until reaching the end or the desired index
        while curr and index > 0:
            curr = curr.next
            index -= 1

        # If index is valid, return the value; else, return -1
        # curr != self.right avoid returning value of right dummy node
        if curr and curr != self.right and index == 0:
            return curr.val

        return -1


    def addAtHead(self, val: int) -> None:
        """
        adds a new node with value val at the head of the list (after the left dummy node).
        """
        # create a new node (ListNode) with the given value
        # new node's next pointer -> first real node (left.next)
        # new node's prev pointer -> left dummy node (left)
        node, next, prev = ListNode(val), self.left.next, self.left

        # dummy node's next is updated to the new node, and the first real node's previous pointer is updated to the new node.
        prev.next = node
        next.prev = node
        node.next = next
        node.prev = prev


    def addAtTail(self, val: int) -> None:
        """
        adds a new node with value val at the tail of the list (before the right dummy node).
        """
        node, next, prev = ListNode(val), self.right, self.right.prev

        # adjust pointers of the surrounding nodes
        prev.next = node
        next.prev = node
        node.next = next
        node.prev = prev


    def addAtIndex(self, index: int, val: int) -> None:
        """
        adds a new node with value val at the specified index.
        """
        curr = self.left.next

        # traverse the list until reaching the end or the desired index
        while curr and index > 0:
            curr = curr.next
            index -= 1

        # if the index is valid, insert the new node at the current position
        if curr and index == 0:
            node, next, prev = ListNode(val), curr, curr.prev

            # adjust pointers of the surrounding nodes
            prev.next = node
            next.prev = node
            node.next = next
            node.prev = prev


    def deleteAtIndex(self, index: int) -> None:
        curr = self.left.next

        # traverse the list until reaching the end or the desired index
        while curr and index > 0:
            curr = curr.next
            index -= 1

        # if the index is valid, delete the node at the current position
        if curr and curr != self.right and index == 0:  # curr != self.right avoids deleting the right dummy node
            next, prev = curr.next, curr.prev
            next.prev = prev
            prev.next = next


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```

- **Time Complexity:** `O(N)` for `get`, `addAtHead`, `addAtTail`, `addAtIndex`, and `deleteAtIndex` operations.
- **Space Complexity:** `O(1)` for all operations.
