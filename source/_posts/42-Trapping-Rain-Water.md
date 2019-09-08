---
title: 42. Trapping Rain Water
date: 2019-09-07 16:48:51
tags:
---

Hard

https://leetcode.com/problems/trapping-rain-water/

Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)
The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image!

**Example:**

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

---

2019.9.7 没做出来，参考 https://www.cnblogs.com/grandyang/p/4402392.html

**方法一：**

先从左往右扫，记录每个位置及其左边的最大高度 left[i]；再从右往左扫，记录每个位置及其右边的最大高度 right[i]。

最后再从左往右扫，则每个位置上的储水高度为 min(left[i], right[i])-height[i]，依次相加即可。

```python
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        if len(height)<=1:
            return 0
        left = [0]*len(height)
        right = [0]*len(height)
        max_h = 0
        for i in range(len(height)):
            max_h = max(max_h, height[i])
            left[i] = max_h
        max_h = 0
        for i in range(len(height)-1, -1, -1):
            max_h = max(max_h, height[i])
            right[i] = max_h
        ans = 0
        for i in range(len(height)):
            ans += max(0, min(left[i], right[i])-height[i])
        return ans
```



**方法二：**

用双指针优化。

1）首先初始化左右指针 l 与 r 为数组首尾，然后左右指针向内移动。

2）若较小值是左指针指向的值，则令 mn=height[l]，并从左向右扫描；若较小值是右指针指向的值，则令 mn=height[r]，则从右向左扫描。

​	扫描过程中若遇到的值比 mn 小，则将差值存入结果，如遇到的值比 mn 大，则重新确定新的窗口范围。

3）以此类推直至左右指针重合，

方法一需要扫三遍数组，方法二只需扫描一遍数组，效率更高。

```python
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        if len(height)<=1:
            return 0
        l,r = 0,len(height)-1
        ans = 0
        while l<r:
            mn = min(height[l], height[r])
            if mn==height[l]:
                l += 1
                while height[l]<mn:
                    ans += mn - height[l]
                    l += 1
            else:
                r -= 1
                while height[r]<mn:
                    ans += mn - height[r]
                    r -= 1
        return ans
```

**类似题目：**

Trapping Rain Water II
Pour Water