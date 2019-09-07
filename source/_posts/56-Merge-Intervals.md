---
title: 56. Merge Intervals
date: 2019-09-04 23:37:12
tags:
---

Medium

https://leetcode.com/problems/merge-intervals/

Given a collection of intervals, merge all overlapping intervals.

**Example 1:**

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

---

2019.9.4 独立做出来了

**方法：**

```python
class Solution(object):
    def merge(self, intervals):
        """
        :type intervals: List[List[int]]
        :rtype: List[List[int]]
        """
        if len(intervals)<=1:
            return intervals
        intervals.sort(key = lambda x:x[0])
        i = 0
        while i<len(intervals)-1:
            if intervals[i][1]<intervals[i+1][0]:
                i += 1
            else:
                intervals[i] = [min(intervals[i][0],intervals[i+1][0]), max(intervals[i][1],intervals[i+1][1])]
                intervals.pop(i+1)
        return intervals
```

**类似题目：**

Insert Interval
Meeting Rooms
Meeting Rooms II
Teemo Attacking
Add Bold Tag in String
Range Module
Employee Free Time
Partition Labels
Interval List Intersections