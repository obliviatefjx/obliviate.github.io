---
title: 84. Largest Rectangle in Histogram
date: 2019-09-08 12:35:25
tags:
---

Hard

https://leetcode.com/problems/largest-rectangle-in-histogram/

Given *n* non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![img](https://assets.leetcode.com/uploads/2018/10/12/histogram.png)
Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

![img](https://assets.leetcode.com/uploads/2018/10/12/histogram_area.png)
The largest rectangle is shown in the shaded area, which has area = `10` unit.

**Example:**

```
Input: [2,1,5,6,2,3]
Output: 10
```

---

2019.9.8 没做出来，参考 https://www.cnblogs.com/lichen782/p/leetcode_Largest_Rectangle_in_Histogram.html 和 https://www.cnblogs.com/grandyang/p/4322653.html

**方法：**

单调递增栈

直方图的矩形面积为 “直方条个数×直方条中高度最小的值”。

（下图转自 https://www.cnblogs.com/lichen782/p/leetcode_Largest_Rectangle_in_Histogram.html，感谢老哥这张配图为我拨开迷雾...）

<img src="https://images0.cnblogs.com/blog/466943/201307/17223405-ba207c5828a54eca8ca81e04175aa3bd.png" width="300px" />

如上图所示，当遇到最后一个递减的直方条 A（红色），那么其前面所有高于它的直方条如果想把 A 也算入矩形面积的话，那么最大的高度也就是 A 的高度了（木桶原理），所以这个时候前面高的直方条再留在这里也没有意义了，可以直接计算一波矩形面积然后移出栈。

比如一些选手（**若干直方条**）组队参加一个比赛（**取得最大矩形**），如果这时又来了一个大佬（**高于前面的所有直方条**），他们就欢迎欢迎，把新来的大佬捧进小组里（**入栈**）。过了一会来了一个选手 A 求带，这时栈里的选手中最强的大佬（栈顶直方条）觉得 A 加进来的话会拉低水平，不乐意。但是按规则只要 A 出现了就必须加进来，所以大佬一合计，继续待在这里是浪费时间，一帮猪队友带不动，干脆打完一把（**计算矩形面积**）就撤了（**出栈**）。最强大佬离开之后之前次强的选手晋升为最强大佬，如果他比 A 强的话会重复前一个大佬的心路历程，直到栈里选手没有比 A 再强的了，然后 A 顺利**入栈**。

注意代码里有两个坑：

1. 栈内元素为直方条的 index（而不是直方条高度）
2. 计算面积时，高为栈顶直方条的高度，宽需要判断一下，详细见代码。

```python
class Solution(object):
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        if len(heights)==0:
            return 0
        if len(heights)==1:
            return heights[0]
        st = []
        heights.append(0)
        ans = 0
        i = 0
        while i<len(heights):
            if len(st)==0 or heights[st[-1]]<=heights[i]:
                st.append(i)
                i += 1
            else:
                temp = st.pop(-1)
                area = heights[temp]*(i-st[-1]-1) if len(st)>0 else heights[temp]*i
                ans = max(ans, area)
        return ans
```

**类似题目：**

Find the Celebrity
Capacity To Ship Packages Within D Days
Grumpy Bookstore Owner