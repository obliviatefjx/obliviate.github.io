---
title: 62. Unique Paths
date: 2019-09-01 23:31:33
tags:
---

Medium

https://leetcode.com/problems/unique-paths/

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)
Above is a 7 x 3 grid. How many possible unique paths are there?

**Note:** *m* and *n* will be at most 100.

**Example 1:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```

---

2019.9.1 独立做出来了

之前面依图的时候被问到了这道题，一开始答的是递归统计所有 paths，后来面试官问有没有更简单的，我不会，最后在面试官的反复提示下我终于答出来了“排列组合”的方法，这道题本质上是数学题（我傻了

**方法：**

对于一个 m 行 n 列的棋盘，从左上角走到右下角一定会走 (m-1)+(n-1) 步，其中会向下走 m-1 步，向右走 n-1 步，所以所有可能的 path 数为：
$$
C_{(m-1)+(n-1)}^{m-1}
$$

```python
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        if m==0 or n==0:
            return 0
        if m==1 or n==1:
            return 1
        p = m-1 + n-1
        q = min(n-1, m-1)
        ans = 1
        for i in range(q,0,-1):
            ans *= p
            p -= 1
        for i in range(q,0,-1):
            ans /= i
        return ans
```



**类似题目：**

Unique Paths II
Dungeon Game