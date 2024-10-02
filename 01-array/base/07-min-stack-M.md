# Min Stack

**Difficulty:** Medium

**Topic:** Stack, Design

**LeetCode Link:** [Min Stack](https://leetcode.com/problems/min-stack/)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- **`int getMin()` retrieves the minimum element in the stack.**

**You must implement a solution with `O(1)` time complexity for each function.**

### Example 1:

```
Input
["MinStack", "push", "push", "push", "getMin", "pop", "top", "getMin"]
[[], [-2], [0], [-3], [], [], [], []]

Output
[null, null, null, null, -3, null, 0, -2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

#### Constraints:

- `-2^31 <= val <= 2^31 - 1`
- Methods `pop`, `top`, and `getMin` operations will always be called on non-empty stacks.
- At most `3 * 10^4` calls will be made to `push`, `pop`, `top`, and `getMin`.

## Approach 1: Stack ✅

We can use two stacks to keep track of the elements and the minimum element. We initialize two stacks, `stack` and `min_stack`. When we push an element onto the stack, we also push the minimum element onto the `min_stack`. When we pop an element from the stack, we also pop the top element from the `min_stack`. We can then retrieve the minimum element in constant time by looking at the top of the `min_stack`.

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        val = min(val, self.min_stack[-1] if self.min_stack else val)
        self.min_stack.append(val)

    def pop(self) -> None:
        self.stack.pop()
        self.min_stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```

- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(n)$
