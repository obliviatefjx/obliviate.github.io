---
title: 309. Best Time to Buy and Sell Stock with Cooldown
date: 2019-08-23 15:34:50
tags:
---

Medium

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

- You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
- After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

**Example:**

```
Input: [1,2,3,0,2]
Output: 3 
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

**方法：**

1. sell 该天结束手里**没有**股票的情况下，已经获得的最大收益
2. buy 该天结束手里**有**股票的情况下，已经获得的最大收益

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices)<=1:
            return 0
        buy = [0] * len(prices)
        sell = [0] * len(prices)
        buy[0] = -prices[0]
        for i in range(1, len(prices)):
            if i<2:
                buy[i] = max(-prices[i], buy[i-1])
            else:
                buy[i] = max(sell[i-2]-prices[i], buy[i-1])
            sell[i] = max(sell[i-1], buy[i-1] + prices[i])
        return sell[-1]
```

