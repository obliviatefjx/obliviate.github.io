---
title: 64. Minimum Path Sum
date: 2019-09-02 20:33:18
tags:
---

Medium

https://leetcode.com/problems/minimum-path-sum/

Given a *m* x *n* grid filled with non-negative numbers, find a path from top left to bottom right which *minimizes* the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example:**

```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

---

2019.9.2 独立做出来了

**方法：**

二维 DP

```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if len(grid)==0 or len(grid[0])==0:
            return 0
        m,n = len(grid), len(grid[0])
        cnt = [[0]*n for _ in range(m)]
        for i in range(m):
            for j in range(n):
                if i==0 and j==0:
                    cnt[i][j] = grid[i][j]
                elif i==0:
                    cnt[i][j] = grid[i][j] + cnt[i][j-1]
                elif j==0:
                    cnt[i][j] = grid[i][j] + cnt[i-1][j]
                else:
                    cnt[i][j] = grid[i][j] + min(cnt[i][j-1], cnt[i-1][j])
        return cnt[-1][-1]
```



**类似题目：**

Dungeon Game
Cherry Pickup