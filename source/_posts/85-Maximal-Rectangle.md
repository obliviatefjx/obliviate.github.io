---
title: 85. Maximal Rectangle
date: 2019-09-08 20:04:58
tags:
---

Hard

https://leetcode.com/problems/maximal-rectangle/

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

**Example:**

```
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
```

---

2019.9.8 独立做出来了，参考 84 题的解法

**方法：**

```python
class Solution(object):
    def maximalRectangle(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        if len(matrix)==0 or len(matrix[0])==0:
            return 0
        m,n = len(matrix), len(matrix[0])
        height = [0]*n
        ans = 0
        for i in range(m):
            for j in range(n):
                if matrix[i][j]=='1':
                    height[j] = int(matrix[i][j]) + height[j]
                else:
                    height[j] = 0
            ans = max(ans, find(height))
        return ans
    
    
def find(nums):
    if len(nums)==0:
        return 0
    if len(nums)==1:
        return nums[0]
    nums.append(0)
    ans = 0
    st = []
    i = 0
    while i<len(nums):
        if len(st)==0 or nums[st[-1]]<=nums[i]:
            st.append(i)
            i += 1
        else:
            temp = st.pop(-1)
            area = nums[temp]*(i-1-st[-1]) if len(st)>0 else nums[temp]*i
            ans = max(ans, area)
    nums.pop(-1)
    return ans
```

**类似题目：**

Paint House
H-Index
Continuous Subarray Sum