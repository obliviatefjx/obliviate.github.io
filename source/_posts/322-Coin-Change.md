---
title: 322. Coin Change
date: 2019-09-18 00:15:36
tags:
---

Medium

https://leetcode.com/problems/coin-change/

You are given coins of different denominations and a total amount of money *amount*. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Example 1:**

```
Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
```

**Note**:
You may assume that you have an infinite number of each kind of coin.

---

2019.9.17 没做出来，参考之前提交的代码（抄的）

**方法：**

1）新建一个长为 amount+1 的数组 ans[]，ans[i] 表示和为 i 的硬币组合里最少的硬币个数。初始化为 a[i] = float('inf')。

2）遍历 ans[1]~ans[amount]，在每次循环中还要遍历每个硬币值，判断“如果把这个硬币放进找零组合里，那么是否能找零且硬币数量最小的组合中的硬币个数是多少”

```python
class Solution(object):
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        """
        if len(coins)==0:
            return -1
        if amount==0:
            return 0
        ans = [float('inf')]*(amount+1)
        ans[0] = 0
        for i in range(1,amount+1):
            for c in coins:
                if c<=i and ans[i-c]!=float('inf'):
                    ans[i] = min(ans[i], ans[i-c]+1)
        return ans[-1] if ans[-1]!=float('inf') else -1
```

**类似题目：**

[Minimum Cost For Tickets](https://leetcode.com/problems/minimum-cost-for-tickets/)

