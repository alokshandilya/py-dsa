# Remove Duplicates from Sorted Array

**Difficulty:** Easy

**Topic:** Array, Two Pointers

**LeetCode Link:** [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only **once**. The **relative order** of the elements should be kept the **same**.

Consider the number of unique elements of `nums` to be `k`, to get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of `nums` contain the unique elements in the order they were present in nums `initially`. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.

### Example 1:

```
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]

Explanation: Your function should return k = 2, with the first two elements
             of nums being 1 and 2 respectively.
             It does not matter what you leave beyond the returned k (hence they are
             underscores).
```

### Example 2:

```
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]

Explanation: Your function should return k = 5, with the first five elements
             of nums being 0, 1, 2, 3, and 4 respectively.
             It does not matter what you leave beyond the returned k (hence they are
             underscores).
```

#### Constraints:

- `0 <= nums.length <= 3 * 10^4`
- `-100 <= nums[i] <= 100`
- `nums` is sorted in **non-decreasing order**.

## Approach 1: Sorting in-place

We can solve using sorting in place using `[:]` and using `set()` to remove duplicates.

```python
def removeDuplicates(nums):
    nums[:] = sorted(set(nums))
    return len(nums)
```

- Time complexity: $O(n \times logn)$
- Space complexity: $O(n)$ _(because of set(nums) call)_

## Approach 2: Two Pointers ✅

We can solve this problem using two pointers. We can keep one pointer (left) at the start of the array and another pointer (right) at index 1.

- If the element at the right pointer is equal to the element at right - 1, meaning it is a duplicate, we will move the right pointer to the next element.
- If the element at the right pointer is not equal to the element at right - 1, meaning  it is not a duplicate, we will move the left pointer to the next element and copy the element at the right pointer to the left pointer.

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return 1
        
        # left for unique elements
        # right for iterating to find unique elements
        left = 0
        
        for right in range(1, len(nums)):
            if nums[right] == nums[right - 1]:
                pass  # right will increase by 1 (loop)
            else:
                # not a duplicate
                nums[left + 1] = nums[right]
                # move left pointer to next (for in-place)
                left += 1
        return left + 1  # count of unique elements
```

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return 1

        left = 0
        for right in range(1, len(nums)):
            if nums[right] != nums[right - 1]:
                nums[left + 1] = nums[right]
                left += 1

        return left + 1
```

- Time complexity: $O(n)$
- Space complexity: $O(1)$
