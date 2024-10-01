# Valid Parentheses

**Difficulty:** Easy

**Topic:** String, Stack

**LeetCode Link:** [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.
- Every close bracket must have an open bracket of the same type.

### Example 1:

```
Input: s = "()[]{}"
Output: true
```

### Example 2:

```
Input: s = "(]"
Output: false
```

### Example 3:

```
Input: s = "([])"
Output: true
```

#### Constraints:

- `1 <= s.length <= 10^4`
- `s` consists of parentheses only `'()[]{}'`.

## Approach 1: Stack ✅

We can use a stack to keep track of the open parentheses. We iterate through the string, and if we encounter an open parentheses, we push it onto the stack. If we encounter a closing parentheses, we check if the top of the stack contains the corresponding open parentheses. If it does, we pop the open parentheses from the stack. If it doesn't, we return `False`. Finally, we return `True` if the stack is empty, and `False` otherwise.

```python
def isValid(s: str) -> bool:
    stack = []
    close_to_open = {")": "(", "}": "{", "]": "["}
    for char in s:
        if char in close_to_open:  # it's a closing parentheses
            if stack and stack[-1] == close_to_open[char]:
                # matching open parentheses
                stack.pop()
            else:
                return False
            if mapping[char] != top_element:
                return False
        else:  # it's an open parentheses
            stack.append(char)
    return True if not stack else False  # stack should be empty
```

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$
