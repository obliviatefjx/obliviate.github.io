---
title: 200. Number of Islands
date: 2019-09-10 00:44:04
tags:
---

Medium

https://leetcode.com/problems/number-of-islands/

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

---

2019.9.10 没做出来，参考 https://blog.csdn.net/fuxuemingzhu/article/details/81126995

**方法：**

看了上面那个博客的讲解：

“我们对每个有“1"的位置进行dfs，把和它四联通的位置全部变成“0”，这样就能把一个点推广到一个岛。所以，我们总的进行了dfs的次数，就是总过有多少个岛的数目。注意理解dfs函数的意义：已知当前是1，把它周围相邻的所有1全部转成0.”

然后自己写的代码。

```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if len(grid)==0 or len(grid[0])==0:
            return 0
        m,n = len(grid), len(grid[0])
        ans = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j]=='1':
                    dfs(grid, i, j)
                    ans += 1
        return ans
    
def dfs(grid, i, j):
    if i<0 or j<0 or i==len(grid) or j==len(grid[0]):
        return
    if grid[i][j]=='1':
        grid[i][j] = '0'
        dfs(grid, i+1, j)
        dfs(grid, i-1, j)
        dfs(grid, i, j+1)
        dfs(grid, i, j-1)
    return 
```

**类似题目：**

Surrounded Regions
Walls and Gates
Number of Islands II
Number of Connected Components in an Undirected Graph
Number of Distinct Islands
Max Area of Island