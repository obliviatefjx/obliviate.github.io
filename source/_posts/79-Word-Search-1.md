---
title: 79. Word Search
date: 2019-09-06 18:31:10
tags:
---

Medium

https://leetcode.com/problems/word-search/

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

---

2019.9.6 独立做出来了

**方法：**

DFS

用一个二维数组 v[i]\[j] 记录 board[i]\[j] 是否被访问过。注意需要在走完一条路径后把 v[i]\[j] 重置为未访问状态。

```python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        if len(board)==0 or len(board[0])==0:
            return False
        m,n = len(board), len(board[0])
        v = [[0]*n for _ in range(m)]
        for i in range(m):
            for j in range(n):
                if search(board, v, m, n, i, j, word, 0):
                    return True
        return False
    
def search(board, v, m, n, i, j, word, pos):
    if i<0 or j<0 or i>=m or j>=n or pos>=len(word):
        return False
    if board[i][j]!=word[pos] or v[i][j]==1:
        return False
    if pos==len(word)-1:
        return True
    v[i][j] = 1
    res = (search(board, v, m, n, i-1, j, word, pos+1) or
           search(board, v, m, n, i+1, j, word, pos+1) or 
           search(board, v, m, n, i, j-1, word, pos+1) or 
           search(board, v, m, n, i, j+1, word, pos+1)
          )
    v[i][j] = 0
    return res
```

**类似题目：**

Word Search II