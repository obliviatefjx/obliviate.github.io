---
title: 240. Search a 2D Matrix II
date: 2019-09-20 19:37:54
tags:
---

Medium

https://leetcode.com/problems/search-a-2d-matrix-ii/

Write an efficient algorithm that searches for a value in an *m* x *n* matrix. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

**Example:**

Consider the following matrix:

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = `5`, return `true`.

Given target = `20`, return `false`.

---

2019.9.20 做出来了

**方法：**

将起始点设置在矩阵右上角，这样从右上角点看整个矩阵，就可以当成一个二叉搜索树 BST。每次比较 matrix\[row]\[col] 和 target 的大小，来二分地向左下角走。

时间复杂度 O(m+n)，其中 m = len(matrix)，n = len(matrix[0])

```python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if len(matrix)==0 or len(matrix[0])==0:
            return False
        row = len(matrix)-1
        col = 0
        while col<len(matrix[0]) and row>=0:
            if matrix[row][col]==target:
                return True
            elif matrix[row][col]>target:
                row -= 1
            else:
                col += 1
        return False
```

**类似题目：**

[Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)