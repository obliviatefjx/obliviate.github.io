---
title: 11. Container With Most Water
date: 2019-09-02 20:51:03
tags:
---

Medium

https://leetcode.com/problems/container-with-most-water/

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

**Example:**

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

---

2019.9.2 没做出来，参考 https://blog.csdn.net/fuxuemingzhu/article/details/82822939

**方法：**

这道题我一开始想到了用双指针，但是不知道当左右两挡板等高的时候怎么处理，讲解是说可以随便移动任意一个，一开始没想明白为什么，和同学讨论之后明白了。

对于目前左、右两个挡板，从两边向中间移动直到相遇。那么只有当向中间移动的挡板遇到了比它更高的板子才“有可能”比之前容量大（因为此时左右挡板间距也缩短了），那么当两挡板一高一矮时，矮版更有可能遇到比它高的，所以向内移动矮版；当两挡板等高时，假设移动左挡板，那么即使左挡板遇到了比它高的板子，只要右挡板不移动，容量也还是会变小，因为容量 = (r-l) * **min**(height[l], height[r])，容器的高仍为右挡板，但宽度（左右挡板间距）减小了，所以容量变小。所以对于两等高挡板来说，只有当两挡板向内移动时都遇到了比它们更高的板子才**“有可能”**比之前容量大，那样的话左右挡板都会向内移动，直到各自遇到比之前高的板子（两个更高的板子还不能是同一个），因此左右哪个板子先向内移动就无所谓了，只是谁先遇到高板子的区别。

```python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        l,r = 0,len(height)-1
        ans = -1
        while l<r:
            ans = max(ans, (r-l)*min(height[l], height[r]))
            if height[l]<height[r]:
                l += 1
            else:
                r -= 1
        return ans
```



**类似题目：**

Missing Ranges
Rotate Array
Can Make Palindrome from Substring