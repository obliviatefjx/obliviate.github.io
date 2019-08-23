---
title: 123. Best Time to Buy and Sell Stock III
date: 2019-08-23 01:39:13
tags:
---

Hard

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete at most *two* transactions.

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**

```
Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
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
        ans = 0
        n_min = float('inf')
        left = [0]*len(prices)
        for i in range(len(prices)):
            n_min = min(n_min, prices[i])
            ans = max(ans, prices[i]-n_min)
            left[i] = ans
        r_ans = 0
        n_max = -float('inf')
        right = [0]*len(prices)
        for i in range(len(prices)-1, -1, -1):
            n_max = max(n_max, prices[i])
            ans = max(ans, n_max-prices[i])
            r_ans = max(r_ans, n_max-prices[i])
            right[i] = r_ans
        
        for i in range(len(prices)):
            ans = max(ans, left[i]+right[i])
        return ans
```

