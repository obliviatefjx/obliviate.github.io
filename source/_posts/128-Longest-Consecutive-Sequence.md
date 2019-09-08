---
title: 128. Longest Consecutive Sequence
date: 2019-09-07 18:10:27
tags:
---

Hard

https://leetcode.com/problems/longest-consecutive-sequence/

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(*n*) complexity.

**Example:**

```
Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

---

2019.9.7 没做出来，参考 https://www.cnblogs.com/zuoyuan/p/3765546.html

**方法：**

1）首先把 nums[] 中的数字存在字典 include{} 中，key 为 数字，value 为 True，表明初始状态下 include{} 中的数字都是可以选取的。

2）遍历 nums[]，对其中的每个数字 n，先判断其之前的连续数字 pre 是否可选取，即 `pre in include and include[pre]`，再判断其之后的连续数字 nxt 是否可选取，即 `nxt in include and include[nxt]`，并在每次判断之后将已判断过的数字置 False。（之所以可以置 False 是因为每个数字只会存在于唯一一个连续数列中，不存在复用的情况，所以用完就扔即可）

3）每次判断的时候用一个变量 cur 记录当前连续数列的长度，并和 ans 进行比较取最大的作为最终 ans 返回。

```python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)<=1:
            return len(nums)
        include = {}
        for n in nums:
            include[n] = True
        ans = 0
        for n in nums:
            cur = 1
            pre = n-1
            while pre in include and include[pre]:
                include[pre] = False
                cur += 1
                pre -= 1
            nxt = n+1
            while nxt in include and include[nxt]:
                include[nxt] = False
                cur += 1
                nxt += 1
            include[n] = False
            ans = max(ans, cur)
        return ans
```

**类似题目：**

Binary Tree Longest Consecutive Sequence