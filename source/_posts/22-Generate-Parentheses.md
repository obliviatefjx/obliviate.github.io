---
title: 22. Generate Parentheses
date: 2019-09-11 00:18:18
tags:
---

Medium

https://leetcode.com/problems/generate-parentheses/

Given *n* pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given *n* = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

---

2019.9.11 独立做出来了

**方法：**

DFS

```python
class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        if n==0:
            return []
        ans = []
        dfs(ans, n, "", 0, 0)
        return ans
    
def dfs(ans, n, st, n_l, n_r):
    if n_l==n and n_r==n:
        ans.append(st)
        return
    if n_r>n or n_l>n or n_l<n_r:
        return
    dfs(ans, n, st+'(', n_l+1, n_r)
    dfs(ans, n, st+')', n_l, n_r+1)
    return
```

**类似题目：**

Combinations
Number of Squareful Arrays
Parsing A Boolean Expression