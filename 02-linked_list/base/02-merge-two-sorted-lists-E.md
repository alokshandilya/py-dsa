# Merge two sorted lists

**Difficulty:** Easy

**Topic:** Linked List, Recursion

**LeetCode Link:** [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

You are given the heads of two sorted linked lists, `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return _the head of the merged linked list_.

### Example 1:

```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

### Example 2:

```
Input: list1 = [], list2 = []
Output: []
```

### Example 3:

```
Input: list1 = [], list2 = [0]
Output: [0]
```

#### Constraints:

- The number of nodes in both lists is in the range `[0, 50]`.
- `-100 <= Node.val <= 100`
- Both `list1` and `list2` are sorted in **non-decreasing** order.

## Approach 1: Iterative ✅

- create a dummy node to simplify handling edge cases (like, when one of the lists is empty).
- with a current pointer tracking the last node of the merged list. we traverse both `list1` and `list2` simultaneously, comparing their current node values.
- at each step, we append the smaller node to the merged list and advance the pointer of the list from which the node was taken.
- once one list is exhausted, we append the remaining nodes of the other list to the merged list, as it's already sorted.
- the result is returned starting from the node after the dummy, as it's just a placeholder.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        current = dummy

        while list1 and list2:
            if list1.val < list2.val:
                current.next = list1
                list1 = list1.next
            else:
                current.next = list2
                list2 = list2.next

            current = current.next

        if list1:
            current.next = list1
        else:
            current.next = list2

        return dummy.next
```

- **Time Complexity:** $O(n + m)$ _(n, m: no. of nodes in `list1`, `list2`)_
- **Space Complexity:** $O(1)$
