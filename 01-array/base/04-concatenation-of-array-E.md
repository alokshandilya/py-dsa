# Concatenation of Array

**Difficulty:** Easy

**Topic:** Array, Simulation

**LeetCode Link:** [Concatenation of Array](https://leetcode.com/problems/concatenation-of-array/)

Given an integer array `nums` of length `n`, you want to create an array `ans` of length `2n` where `ans[i] == nums[i]` and `ans[i + n] == nums[i]` for `0 <= i < n` **(0-indexed)**.

Specifically, `ans` is the concatenation of two `nums` arrays.

Return the array `ans`.

### Example 1:

```
Input: nums = [1,2,1]
Output: [1,2,1,1,2,1]

Explanation: The array ans is formed as follows:
             - ans = [nums[0],nums[1],nums[2],nums[0],nums[1],nums[2]]
             - ans = [1,2,1,1,2,1]
```

### Example 2:

```
Input: nums = [1,3,2,1]
Output: [1,3,2,1,1,3,2,1]

Explanation: The array ans is formed as follows:
             - ans = [nums[0],nums[1],nums[2],nums[3],nums[0],nums[1],nums[2],nums[3]]
             - ans = [1,3,2,1,1,3,2,1]
```

#### Constraints:

- `n == nums.length`
- `1 <= n <= 1000`
- `1 <= nums[i] <= 1000`

## Approach 1: Brute Force

We can solve this problem using a brute force approach. We can create an empty array and iterate over the array `nums`. We can then append the elements of the array `nums` to the empty array in the required order. We can then return the combined array.

```python
def getConcatenation(nums):
    ans = []
    for i in range(len(nums)):
        ans.append(nums[i])
    for i in range(len(nums)):
        ans.append(nums[i])
    return ans
```

- Time Complexity: $O(n)$
- Space Complexity: $O(n)$

## Approach 2: Concatenation of Array ✅

We can solve this problem using a more optimized approach. We can create an empty array of size `2n` and iterate over the array `nums`. We can then append the elements of the array `nums` to the empty array in the required order. We can then return the combined array.

```python
def getConcatenation(nums):
    n = len(nums)
    ans = [0] * (2 * n)
    for i in range(n):
        ans[i] = nums[i]
        ans[i + n] = nums[i]
    return ans
```

or, we can use the `+` operator to concatenate the arrays.

```python
def getConcatenation(nums):
    return nums + nums
```

- Time Complexity: $O(n)$
- Space Complexity: $O(n)$
