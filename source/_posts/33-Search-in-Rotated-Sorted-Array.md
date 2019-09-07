---
title: 33. Search in Rotated Sorted Array
date: 2019-09-05 18:09:03
tags:
---

Medium

https://leetcode.com/problems/search-in-rotated-sorted-array/

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

You are given a target value to search. If found in the array return its index, otherwise return `-1`.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

---

2019.9.5 没做出来（二分查找的题好难啊...！参考 https://blog.csdn.net/fuxuemingzhu/article/details/79534213

**方法：**

二分查找的变体，先通过比较 nums[left] 与 nums[mid] 的大小来判断旋转点在 mid 左侧还是在 mid 右侧。

若 nums[left] <= nums[mid]，表明 mid 左侧有序，这时判断 target 是否在有序区间内，若不在则 target 在 mid 右侧；

若 nums[left] > nums[mid]，表明 mid 右侧有序，这时判断 target 是否在有序区间内，若不在则 target 在 mid 左侧；

```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if len(nums)==0:
            return -1
        if len(nums)==1:
            return 0 if nums[0]==target else -1
        l,r = 0,len(nums)-1
        while l<=r:
            mid = l+(r-l)/2
            if nums[mid]==target:
                return mid
            if nums[l]<=nums[mid]:
                if nums[mid]>target and nums[l]<=target:
                    r = mid-1
                else:
                    l = mid+1
            else:
                if nums[mid]<target and nums[r]>=target:
                    l = mid+1
                else:
                    r = mid-1
        return -1
```

**类似题目：**

Search in Rotated Sorted Array II
Find Minimum in Rotated Sorted Array