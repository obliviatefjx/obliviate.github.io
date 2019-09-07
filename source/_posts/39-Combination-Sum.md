---
title: 39. Combination Sum
date: 2019-09-01 18:29:19
tags:
---

Medium

https://leetcode.com/problems/combination-sum/

Given a **set** of candidate numbers (`candidates`) **(without duplicates)** and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sums to `target`.

The **same** repeated number may be chosen from `candidates` unlimited number of times.

**Note:**

- All numbers (including `target`) will be positive integers.
- The solution set must not contain duplicate combinations.

**Example:**

```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

---

2019.9.1 独立做出来了

**方法：**

采用递归方法。

先对 candidates[] 排序，然后从大到小判断，需要注意的是由于可以同一个数字多次出现，所以递归时传入的 candidates[] 是 candidates[0:i+1]

```python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        candidates.sort()
        if len(candidates)==0 or target<candidates[0]:
            return []
        ans = []
        for i in range(len(candidates)-1 ,-1, -1):
            temp = target - candidates[i]
            if temp==0:
                ans.append([candidates[i]])
            elif temp>0:
                res = self.combinationSum(candidates[0:i+1], temp)
                if len(res)>0:
                    for r in res:
                        r.append(candidates[i])
                        ans.append(r)
        return ans
```



**类似题目：**

Combination Sum II
Combinations
Combination Sum III
Factor Combinations
Combination Sum IV