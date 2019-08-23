---
title: 714. Best Time to Buy and Sell Stock with Transaction Fee
date: 2019-08-23 23:32:10
tags:
---

Medium

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/

Your are given an array of integers `prices`, for which the `i`-th element is the price of a given stock on day `i`; and a non-negative integer `fee`representing a transaction fee.

You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction. You may not buy more than 1 share of a stock at a time (ie. you must sell the stock share before you buy again.)

Return the maximum profit you can make.

**Example 1:**

```
Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
Buying at prices[0] = 1Selling at prices[3] = 8Buying at prices[4] = 4Selling at prices[5] = 9The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

**方法：**

```python
class Solution(object):
    def maxProfit(self, prices, fee):
        """
        :type prices: List[int]
        :type fee: int
        :rtype: int
        """
        if len(prices)<=1:
            return 0
        sell = [0]*len(prices)
        buy = [0]*len(prices)
        buy[0] = -prices[0]-fee
        for i in range(1, len(prices)):
            sell[i] = max(sell[i-1], buy[i-1]+prices[i])
            buy[i] = max(sell[i-1]-prices[i]-fee, buy[i-1])
        return sell[-1]
```

