---
title: 54. Spiral Matrix
date: 2019-09-01 01:33:01
tags:
---

Medium

https://leetcode.com/problems/spiral-matrix/

Given a matrix of *m* x *n* elements (*m* rows, *n* columns), return all elements of the matrix in spiral order.

**Example:**

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```

---

2019.9.1 没做出来，一碰到矩阵坐标相关的题就懵QAQ，参考 https://www.cnblogs.com/grandyang/p/4362675.html 

P.S. 这位博主那句 “这道题让我们搓一个螺旋丸” 笑死我了hhhh

这道题的代码我几乎是照着参考答案照抄的，迷迷糊糊，还需要再多看几遍

**方法：**

```python
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        if len(matrix)==0 or len(matrix[0])==0:
            return []
        m = len(matrix)
        n = len(matrix[0])
        ans = []
        cnt = (min(m,n)+1)/2
        p,q = m,n
        for i in range(cnt):
            for col in range(i,i+q):
                ans.append(matrix[i][col])
            for row in range(i+1,i+p):
                ans.append(matrix[row][i+q-1])
            if p==1 or q==1:
                break
            for col in range(i+q-2, i, -1):
                ans.append(matrix[i + p - 1][col])
            for row in range(i+p-1, i, -1):
                ans.append(matrix[row][i])
            q -= 2
            p -= 2
        return ans
```



**类似题目：**

Spiral Matrix II
Spiral Matrix III

