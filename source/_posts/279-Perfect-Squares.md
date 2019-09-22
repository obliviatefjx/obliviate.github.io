---
title: 279. Perfect Squares
date: 2019-09-17 23:51:30
tags:
---

Medium

https://leetcode.com/problems/perfect-squares/

Given a positive integer *n*, find the least number of perfect square numbers (for example, `1, 4, 9, 16, ...`) which sum to *n*.

**Example 1:**

```
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```

---

2019.9.17 做出来了

感觉这道题和 322. Coin Change 一样一样的，但是官方的“类似题目”里又没出现 Coin Change...（这两道题真的好像呀

方法也是照搬的 Coin Change 的解法，但是 Coin Change 我之前没做出来，所以这道题的“做出来了”比较虚hhhh

**方法：**（有点像恰好装满的背包问题）

1）求 n 的开方值 high，所以平方和为 n 的可能组合中的数字最大不超过 high。

2）新建一个长为 n+1 的数组 ans[]，ans[i] 表示平方和为 i 的数字组合里最少的数字个数。因此初始化为 a[i] = i，表示最开始最多是 i 个 1 的平方和为 i。

3）遍历 a[1]~a[n]，在每次循环中还要从小到大遍历 1~high，判断“如果把这个数放进平方和组合里，那么数字数量最小的组合中的数字个数是多少”

P.S. 我看到有另外一种[非常简单的方法](https://www.cnblogs.com/grandyang/p/4800552.html)，用到了 “四平方和定理”，没再深究了。

```python
class Solution(object):
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n==1:
            return 1
        ans = [i for i in range(n+1)]
        high = int(n**0.5)
        for i in range(1,n+1):
            for j in range(1,high+1):
                if j*j<=i:
                    ans[i] = min(ans[i], ans[i-j*j]+1)
        return ans[-1]
```

**类似题目：**

Count Primes
Ugly Number II