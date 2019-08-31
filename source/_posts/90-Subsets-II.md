---
title: 90. Subsets II
date: 2019-08-30 00:29:12
tags:
---

Medium

https://leetcode.com/problems/subsets-ii/

Given a collection of integers that might contain duplicates, **nums**, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

--------------

**2019.8.30** - 没做出来，参考 https://www.cnblogs.com/grandyang/p/4310964.html 后写出来了

方法和 78. Subsets 类似，但需增加一个去重操作：“用 last 来记录上一个处理的数字，然后判定当前的数字和上面的是否相同，若不同，则循环还是从0到当前子集的个数，若相同，则新子集个数减去之前循环时子集的个数当做起点来循环，这样就不会产生重复了”

要点：因为求的是 the power set（幂集），也就是说两个子集只要包含的数字相同就算是相同的，e.g. [1,4,1] 和 [1,1,4] 是相同的，所以需要先对 nums[] 排序，这样就保证了求的是幂集。

```python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums)==0:
            return [[]]
        nums.sort()
        ans = [[]]
        last = nums[0]
        last_len = 1
        for i in range(len(nums)):
            if nums[i]!=last:
                last = nums[i]
                last_len = len(ans)
            len_ = len(ans)
            for j in range(len_-last_len, len_):
                new = copy.deepcopy(ans[j])
                new.append(nums[i])
                ans.append(new)
        return ans
```

这是非递归解，还有一种 DFS 解没有写。



**类似题目：**

