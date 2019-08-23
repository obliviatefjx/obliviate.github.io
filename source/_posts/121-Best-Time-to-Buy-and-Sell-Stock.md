---
title: 121. Best Time to Buy and Sell Stock
date: 2019-08-23 00:42:02
tags:
---

Easy

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

**方法：**

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices)==1:
            return 0
        n_min = float('inf')
        ans = 0
        for n in prices:
            n_min = min(n, n_min)
            ans = max(ans, n-n_min)
        return ans
```



**类似题目：**

\122. Best Time to Buy and Sell Stock II