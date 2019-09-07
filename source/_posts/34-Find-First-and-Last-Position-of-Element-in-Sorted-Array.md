---
title: 34. Find First and Last Position of Element in Sorted Array
date: 2019-09-05 00:25:49
tags:
---

Medium

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

If the target is not found in the array, return `[-1, -1]`.

**Example:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

---

2019.9.5 没做出来，思路参考 https://www.cnblogs.com/grandyang/p/4409379.html，但按照自己的理解写的

**方法：**

二分查找的边界条件好容易写错啊，一不小心就 bug 了。看了 [彻底理解二分查找及其边界情况](http://www.codebelief.com/article/2018/04/completely-understand-binary-search-and-its-boundary-cases/) 和 [二分查找学习札记](http://www.cppblog.com/converse/archive/2009/10/05/97905.html) 两篇博文之后理解了一些。

二分查找有三个坑容易踩：初始化左右指针、mid 计算方式、更新左右指针的比较条件。（其实还有一个坑是退出循环的条件但不太容易踩就没写上）

【以下仅针对区间是一开一闭的情况】

1. **左闭右开——找第一次出现的位置**

   1）初始化左右指针：

   左闭右开，即左指针能取到，右指针取不到。

   ```python
   l,r = 0,len(nums)
   ```

   2）mid 计算方式：

   向下取整。

   由于 Java 语言（C、C++、Python 等也一样）的除法是自动向下取整，因此中间位置 mid 会偏向左边界 left，所以 right = mid 而不是 right = mid - 1。因为只要 left 和 right 不相等，right = mid 一定会较原来的 right 左移，这样可以确保范围不断缩小。

   ```python
   mid = l+(r-l)/2
   ```

   3）更新左右指针的比较条件：

   当 mid 处的值大于或等于目标值时，将右边界左移；只有 mid 处的值明确小于目标值时，才被动将左边界右移，这样就能尽可能地让右边界往左移动。

   ```python
   if nums[mid]<target:
       l = mid+1
   else:
       r = mid
   ```

   **总代码：**

   ```python
       def searchFirst(nums, target):
           """
           :type nums: List[int]
           :type target: int
           :rtype: List[int]
           """
           l,r = 0,len(nums)
           while l<r:
               mid = l+(r-l)/2
               if nums[mid]<target:
                   l = mid+1
               else:
                   r = mid
           return l
   ```



2. **左开右闭——找最后一次出现的位置**

   1）初始化左右指针：

   左开右闭，即左指针取不到，右指针能取到。

   ```python
   l,r = -1,len(nums)-1
   ```

   2）mid 计算方式：

   向上取整，**需加 1**

   虽然 Java 本身的除法是自动向下取整，但是我们可以先将被除数加一之后再做除法，这样就等价于向上取整，mid 会偏向右边界，因此 left = mid 可以确保左边界往右移动，缩小查找范围。

   ```python
   mid = l+(r-l+1)/2
   ```

   3）更新左右指针的比较条件：

   当 mid 处的值小于或等于目标值时，将左边界右移；只有 mid 处的值明确大于目标值时，才被动将右边界左移，这样就能尽可能地让左边界往右移动。

   ```python
   if nums[mid]>target:
       r = mid-1
   else:
       l = mid
   ```

   **总代码：**

   ```python
       def searchLast(nums, target):
           """
           :type nums: List[int]
           :type target: int
           :rtype: List[int]
           """
           l,r = -1,len(nums)-1
           while l<r:
               mid = l+(r-l+1)/2
               if nums[mid]>target:
                   r = mid-1
               else:
                   l = mid
           return l
   ```



回到原题，最终代码为上述两套代码的串行：

```python
class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if len(nums)==0:
            return [-1,-1]
        if len(nums)==1:
            if nums[0]==target:
                return [0,0]
            else:
                return [-1,-1]
        ans = [-1,-1]
        l,r = 0,len(nums)
        while l<r:
            mid = l+(r-l)/2
            if nums[mid]<target:
                l = mid+1
            else:
                r = mid
        if r==len(nums) or nums[r]!=target:
            return ans
        ans[0] = l
        
        r = len(nums)-1
        while l<r:
            mid = l+(r-l+1)/2
            if nums[mid]>target:
                r = mid-1
            else:
                l = mid
        ans[1] = r
        return ans
```



**类似题目：**

First Bad Version