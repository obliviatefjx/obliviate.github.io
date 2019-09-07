---
title: 31. Next Permutation
date: 2019-09-06 19:36:55
tags:
---

Medium

https://leetcode.com/problems/next-permutation/

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be **in-place** and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

---

2019.9.6 独立做出来了，但是调了半天 bug

**方法：**

1）从右往左扫，直到在某个位置 idx 上，nums[idx-1]<nums[idx]。那么左边待移动的元素就是 nums[idx-1]，令 left=idx-1。

2）然后再从 idx 向右扫，直到 nums[idx]<=nums[left]，那么右边待移动的元素就为 nums[idx-1]，令 right=idx-1。

3）交换 nums[left] 与 nums[right] 的值。

4）把 left 之后的数组反转一下。

```python
class Solution(object):
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        if len(nums)<1:
            return
        r = len(nums)-1
        while r>0 and nums[r-1]>=nums[r]:
            r -= 1
        if r==0:
            reverse(nums, 0, len(nums)-1)
            return
        l = r-1
        while r<len(nums) and nums[r]>nums[l]:
            r += 1
        r -= 1
        nums[l], nums[r] = nums[r], nums[l]
        reverse(nums, l+1, len(nums)-1)
        return
```

**类似题目：**

Permutations II
Permutation Sequence
Palindrome Permutation II