---
title: 48. Rotate Image
date: 2019-09-01 23:23:12
tags:
---

Medium

https://leetcode.com/problems/rotate-image/

You are given an *n* x *n* 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

**Note:**

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example:**

```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

---

2019.9.1 独立做出来了

**方法：**

感觉这道题和打印螺旋数组的题有些类似，重点就是搞清坐标变换（我总是搞混...

从四周向中心依次旋转每层，对每个坐标 replace 它四边上的值。

（下图引用自 https://blog.csdn.net/happyaaaaaaaaaaa/article/details/51563752）

![img](D:\github\obliviatefjx.github.io\images\Center)

```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        if len(matrix)==0 or len(matrix[0])==0:
            return matrix
        n = len(matrix)
        for i in range(n/2):
            for j in range(i, n-i-1):
                temp = matrix[i][j]
                matrix[i][j] = matrix[n-j-1][i]
                matrix[n-j-1][i] = matrix[n-i-1][n-j-1]
                matrix[n-i-1][n-j-1] = matrix[j][n-i-1]
                matrix[j][n-i-1] = temp
        return matrix
```



**类似题目：**

Triangle
Available Captures for Rook
Uncrossed Lines