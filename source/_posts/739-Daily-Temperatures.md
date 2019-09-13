---
title: 739. Daily Temperatures
date: 2019-09-12 01:09:49
tags:
---

Medium

https://leetcode.com/problems/daily-temperatures/Given a list of daily temperatures `T`, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put `0` instead.

For example, given the list of temperatures `T = [73, 74, 75, 71, 69, 72, 76, 73]`, your output should be `[1, 1, 4, 2, 1, 1, 0, 0]`.

**Note:** The length of `temperatures` will be in the range `[1, 30000]`. Each temperature will be an integer in the range `[30, 100]`.

---

2019.9.12 独立做出来了

**方法：**

单调递减栈

```python
class Solution(object):
    def dailyTemperatures(self, T):
        """
        :type T: List[int]
        :rtype: List[int]
        """
        if len(T)==1:
            return [0]
        ans = [0]*len(T)
        st = []
        i = 0
        while i<len(T):
            if len(st)==0 or T[st[-1]]>=T[i]:
                st.append(i)
                i += 1
            else:
                temp = st.pop(-1)
                ans[temp] = i-temp
        return ans
```

**类似题目：**

[Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)