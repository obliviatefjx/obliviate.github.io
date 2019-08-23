---
title: 122. Best Time to Buy and Sell Stock II
date: 2019-08-23 00:58:04
tags:
---

Easy

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

**方法一：**

2019-8-23 自己写的

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices)==1:
            return 0
        day = 0
        ans = 0
        while day<len(prices):
            while day<len(prices)-1 and prices[day]>=prices[day+1]:
                day += 1
            if day==len(prices)-1:
                break
            cur_p = prices[day]
            while day<len(prices)-1 and prices[day]<=prices[day+1]:
                day += 1
            ans += prices[day]-cur_p
            if day==len(prices)-1:
                break
            day += 1
        return ans
```

方法二：

2019-8-23 参考 https://www.cnblogs.com/grandyang/p/4280803.html

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices)==1:
            return 0
        ans = 0
        for i in range(len(prices)-1):
            ans += max(0, prices[i+1]-prices[i])
        return ans
```

