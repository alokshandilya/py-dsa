# Remove Element

**Difficulty:** Easy

**Topic:** Array, Two Pointers

**LeetCode Link:** [Remove Element](https://leetcode.com/problems/remove-element/)

Given an interger array `nums` and an integer `val`, remove all occurrences of `val` in `nums` **in-place**. The order of the elements may be changed. Then return _the number of elements in_ `nums` _which are not equal to_ `val`.

Consider the number of elements in `nums` which are not equal to `val` to be `k`, to get accepted, you need to do the following things:

- change the array `nums` such that the first `k` elements of `nums` contain the elements that are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
- return `k`.

### Example 1:

```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]

Explanation: Your function should return k = 2, with the first two elements
             of nums being 2 and 2 respectively.
             It does not matter what you leave beyond the returned k (hence they are
             underscores).
```

### Example 2:

```
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]

Explanation: Your function should return k = 5, with the first five elements
             of nums containing 0, 0, 1, 3, and 4.
             Note that the five elements can be returned in any order.
             It does not matter what you leave beyond the returned k (hence they are
             underscores).
```

#### Constraints:

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

## Approach 1: Using Python's `remove()` method

We can solve this problem using Python's `remove()` method. We can iterate over the array and remove the element `val` using the `remove()` method. We can then return the length of the array.

```python
def removeElement(nums, val):
    while val in nums:
        nums.remove(val)
    return len(nums)
```

- Time complexity: $O(n^2)$
- Space complexity: $O(1)$

## Approach 2: Using Python's `list comprehension`

We can solve this problem using Python's list comprehension. We can filter out the elements that are not equal to `val` and then return the length of the array.

```python
def removeElement(nums, val):
    nums[:] = [x for x in nums if x != val]
    return len(nums)
```

- Time complexity: $O(n)$
- Space complexity: $O(n)$ _(because of list comprehension)_

## Approach 3: Two Pointers ✅

We can solve this problem using two pointers. We can keep one pointer `i` for iterating over the array and another pointer `k` for keeping track of the elements that are not equal to `val`. We can then swap the elements at `i` and `k` if `nums[i]` is not equal to `val`. We can then increment `k` and `i` by 1.

```python
def removeElement(nums, val):
    k = 0
    for i in range(len(nums)):
        if nums[i] != val:
            nums[k], nums[i] = nums[i], nums[k]
            k += 1
    return k
```

- Time complexity: $O(n)$
- Space complexity: $O(1)$
