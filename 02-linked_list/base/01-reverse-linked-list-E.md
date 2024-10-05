# Reverse Linked List

**Difficulty:** Easy

**Topic:** Linked List, Recursion

**LeetCode Link:** [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

Given the `head` of a singly linked list, reverse the list, and return the reversed list.

### Example 1:

```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

### Example 2:

```
Input: head = []
Output: []
```

#### Constraints:

- The number of nodes in the list is the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`

## Approach 1: Iterative ✅

We can reverse the linked list iteratively by maintaining three pointers: `prev`, `curr`, and `next`. We start by setting `prev` to `None` and `curr` to the `head`. We then iterate through the linked list, updating the `next` pointer to the next node, setting the `curr` node's `next` pointer to `prev`, and updating `prev` and `curr` to the next nodes. We continue this process until we reach the end of the linked list.

```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        prev = None
        curr = head
        while curr:
            next_node = curr.next
            curr.next = prev
            prev = curr
            curr = next_node
        return prev
```

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$

## Approach 2: Recursive ✅

We can reverse the linked list recursively by calling the `reverseList` function on the next node and updating the next node's `next` pointer to the current node. We continue this process until we reach the end of the linked list, at which point we return the new head of the reversed list.

```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        new_head = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return new_head
```

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$ _(due to the recursive stack)_
