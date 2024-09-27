# Shuffle the Array

**Difficulty:** Easy

**Topic:** Array

**LeetCode Link:** [Shuffle the Array](https://leetcode.com/problems/shuffle-the-array/)

Given the array `nums` consisting of `2n` elements in the form `[x1,x2,...,xn,y1,y2,...,yn]`.

_Return the array in the form_ `[x1,y1,x2,y2,...,xn,yn]`.

### Example 1:

```
Input: nums = [2,5,1,3,4,7], n = 3
Output: [2,3,5,4,1,7]

Explanation: Since x1=2, x2=5, x3=1, y1=3, y2=4, y3=7 then the answer is [2,3,5,4,1,7].
```

### Example 2:

```
Input: nums = [1,2,3,4,4,3,2,1], n = 4
Output: [1,4,2,3,3,2,4,1]
```

### Example 3:

```
Input: nums = [1,1,2,2], n = 2
Output: [1,2,1,2]
```

#### Constraints:

- `1 <= n <= 500`
- `nums.length == 2n`
- `1 <= nums[i] <= 10^3`

## Approach 1: Brute Force ✅

We can solve this problem using a brute force approach. We can create an empty array and iterate over the array `nums`. We can then append the elements of the array `nums` to the empty array in the required order. We can then return the combined array.

```python
def shuffle(nums, n):
    result = []
    for i in range(n):
        result.append(nums[i])
        result.append(nums[i+n])
    return result
```

We can also solve this problem using **Python's `extend()` method**. We can iterate over the array and use the `extend()` method to combine the elements of the array. We can then return the combined array.

```python
def shuffle(nums, n):
    result = []
    for i in range(n):
        result.extend([nums[i], nums[i+n]])
    return result
```

We can also solve this problem using **two pointers**. We can create two pointers `i` and `j` and iterate over the array `nums`. We can then append the elements of the array `nums` to the empty array in the required order. We can then return the combined array.

```python
def shuffle(nums, n):
    result = []
    i, j = 0, n
    for _ in range(n):
        result.append(nums[i])
        result.append(nums[j])
        i += 1
        j += 1
    return result
```

- Time complexity: $O(n)$
- Space complexity: $O(n)$

## Approach 2: Bit Manipulation (for constant space)

We can solve this problem using bit manipulation. We can iterate over the array `nums` and use the bitwise OR operator to combine the elements of the array. We can then use the bitwise right shift operator to extract the elements of the array. We can then return the combined array.

- [video explanation](https://www.youtube.com/watch?v=IvIKD_EU8BY)

```python
def shuffle(nums, n):
    for i in range(n):
        nums[i] = nums[i] << 10
        nums[i] = nums[i] | nums[i+n]  # store x, y (combine)

    j = 2 * n - 1
    for i in range(n - 1, -1, -1):
        y = nums[i] & (2**10 - 1)  # extract y
        x = nums[i] >> 10  # extract x
        nums[j] = y
        nums[j - 1] = x
        j -= 2
    return nums
```

- Time complexity: $O(n)$
- Space complexity: $O(1)$
