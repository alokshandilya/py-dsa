# Baseball Game

**Difficulty:** Easy

**Topic:** Array, Stack, Simulation

**LeetCode Link:** [Baseball Game](https://leetcode.com/problems/baseball-game/)

You are keeping score for a baseball game with strange rules. At the beginning of the game, you start with an empty record.

You are given a list of strings `operations`, where `operations[i]` is the `ith` operation you must apply to the record and is one of the following:

- An integer `x`
  - Record a new score of `x`.
- `"+"`
  - Record a new score that is the sum of the previous two scores.
- `"D"`
  - Record a new score that is double the previous score.
- `"C"`
  - Invalidate the previous score, removing it from the record.

Return _the sum of all the scores on the record after all the operations._

The answer is guaranteed to fit in a 32-bit integer.

### Example 1:

```
Input: operations = ["5","2","C","D","+"]
Output: 30

Explanation:
- "5" - Add 5 to the record, record is now [5].
- "2" - Add 2 to the record, record is now [5, 2].
- "C" - Invalidate and remove the previous score, record is now [5].
- "D" - Add 2 * 5 = 10 to the record, record is now [5, 10].
- "+" - Add 5 + 10 = 15 to the record, record is now [5, 10, 15].
The total sum is 5 + 10 + 15 = 30.
```

### Example 2:

```
Input: operations = ["1","C"]
Output: 0

Explanation:
- "1" - Add 1 to the record, record is now [1].
- "C" - Invalidate and remove the previous score, record is now [].
The total sum is 0.
```

#### Constraints:

- `1 <= operations.length <= 1000`
- `operations[i]` is `"C"`, `"D"`, `"+"`, or a string representing an integer in the range `[-3 * 10^4, 3 * 10^4]`.
- For operation `"+"` there will always be at least two previous scores on the record.
- For operations `"C"` and `"D"`, there will always be at least one previous score on the record.

## Approach 1: Brute Force ✅

We can solve this problem using a brute force approach. We can create an empty **array/stack** and iterate over the array `operations`. We can then perform the required operation on the array and calculate the sum of the array. We can then return the sum of the array.

```python
def calPoints(operations):
    record = []
    for op in operations:
        if op == "C":
            record.pop()
        elif op == "D":
            record.append(2 * record[-1])
        elif op == "+":
            record.append(record[-1] + record[-2])
        else:
            record.append(int(op))
    return sum(record)
```

- Time Complexity: $O(n)$
- Space Complexity: $O(n)$
