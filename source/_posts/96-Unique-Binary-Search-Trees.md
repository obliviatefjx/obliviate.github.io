---
title: 96. Unique Binary Search Trees
date: 2019-09-17 13:02:47
tags:
---

Medium

https://leetcode.com/problems/unique-binary-search-trees/

Given *n*, how many structurally unique **BST's** (binary search trees) that store values 1 ... *n*?

**Example:**

```
Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

---

2019.9.17 做出来了

**方法：**

卡特兰数

```python
class Solution(object):
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n<=1:
            return 1
        dp = [0]*(n+1)
        dp[0] = 1
        dp[1] = 1
        for i in range(2,n+1):
            for j in range(i):
                dp[i] += dp[j]*dp[i-j-1]
        return dp[-1]
```

**类似题目：**

[Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)