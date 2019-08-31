---
title: 78. Subsets
date: 2019-08-29 00:23:09
tags:
---

Medium

https://leetcode.com/problems/subsets/

Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```



---------------

2019.08.29 独立做出来

```python
import copy
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums)==0:
            return [[]]
        ans = [[]]
        for n in nums:
            len_ = len(ans)
            for i in range(len_):
                new = copy.deepcopy(ans[i])
                new.append(n)
                ans.append(new)
        return ans
```



---------------------

**类似题目：**

Subsets II
Generalized Abbreviation
Letter Case Permutation