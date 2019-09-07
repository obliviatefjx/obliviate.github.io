---
title: 55. Jump Game
date: 2019-09-06 18:11:36
tags:
---

Medium

https://leetcode.com/problems/jump-game/

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example:**

```
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

---

2019.9.6 没做出来，参考 https://blog.csdn.net/fuxuemingzhu/article/details/83504437

**方法：**

思路是用一个变量 sum_ 表示当前能到达的最大 index，并在每个位置上判断当前 index 是否超过 sum\_，若超过则无法到达，并在每次判断完后更新 sum\_。

**注意更新 sum\_ 为 sum\_ = max(sum_, i+nums[i])。**我一开始把更新方式错写成了 sum\_ += nums[i]，就 gg 了。

```python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums)==0:
            return False
        if len(nums)==1:
            return True
        sum_ = 0
        for i in range(len(nums)):
            if sum_<i:
                return False
            sum_ = max(sum_, i+nums[i])
        return True
```

**类似题目：**

Jump Game II

