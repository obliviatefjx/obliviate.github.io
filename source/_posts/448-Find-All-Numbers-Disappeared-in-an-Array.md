---
title: "448. Find All Numbers Disappeared in an Array"
date: 2019-08-22 19:57:24
tags:
---

Easy

https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/

**题目描述：**

Given an array of integers where 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear twice and others appear once.

Find all the elements of [1, *n*] inclusive that do not appear in this array.

Could you do it without extra space and in O(*n*) runtime? You may assume the returned list does not count as extra space.

**Example:**

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

**方法：**

由题目可以知道，数组中的数字均满足1 ≤ a[i] ≤ n，也就是说其中的元素和数组的位置索引存在某种关联性。如果数组中不缺少数字，那么每一个元素就会与数组的位置索引所一一对应，那么我们就可以利用这种关系。

将 nums[i] 置换到其对应的位置 nums[nums[i]-1] 上去，比如对于没有缺失项的正确的顺序应该是 [1, 2, 3, 4, 5, 6, 7, 8]，而我们现在却是 [4,3,2,7,8,2,3,1]，我们需要把数字移动到正确的位置上去，比如第一个 4 就应该和 7 先交换个位置，以此类推，最后得到的顺序应该是 [1, 2, 3, 4, 3, 2, 7, 8]，我们最后在对应位置检验，如果 nums[i] 和 i+1 不等，那么我们将 i+1 存入结果 ans 中即可。

```python
class Solution(object):
    def findDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        i = 0
        while i<len(nums):
            if nums[i]!=nums[nums[i]-1]:
                nums[nums[i]-1], nums[i] = nums[i], nums[nums[i]-1]
                i -= 1
            i += 1
        ans = []
        for i in range(len(nums)):
            if nums[i]!=i+1:
                ans.append(nums[i])
        return ans
```



**类似题：**

First Missing Positive

Find the Duplicate Number

Find All Duplicates in an Array



