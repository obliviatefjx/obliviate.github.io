---
title: 41. First Missing Positive
date: 2019-09-09 00:53:17
tags:
---

Hard

https://leetcode.com/problems/first-missing-positive/

Given an unsorted integer array, find the smallest missing positive integer.

**Example:**

```
Input: [1,2,0]
Output: 3
```

**Note:**

Your algorithm should run in *O*(*n*) time and uses constant extra space.

---

2019.9.9 独立做出来了

~~堂堂一道 hard 题竟然被我做出来了，想想还有点小激动？~~

**方法：**

方法和 448 题类似，由于要求 O(n) 时间复杂度和 O(1) 空间复杂度，只能想到查找，要么指针要么元素交换，元素交换的话就需要把元素值和 index 联系起来。

同时又想到对于一个长度为 N 的数组 nums[] 来说，其返回的最大 missing positive integer 也就是 N+1（当 nums[i] = i + 1 时），因此可以遍历数组，把非法元素值（nums[i] <= 0 或 nums[i] > N 的值）滤掉，同时把合法元素值按 index 交换。最后再遍历一遍数组，返回第一次出现 nums[i] != i + 1 时的 i+1 值。

> 这道题我一开始提交的代码一直显示超时，我还以为是算法问题，按照别人的标答提交也还是超时，最后定位出 bug 是在交换 nums[i] 和 nums[nums[i]-1] 时的代码上：
>
> 我写的是 `nums[i], nums[nums[i]-1] = nums[nums[i]-1], nums[i]` ，**超时**。
>
> 改成
>
> ```python
> temp = nums[nums[i]-1]
> nums[nums[i]-1] = nums[i]
> nums[i] = temp`
> ```
>
> **AC**。
>
> 原因可参考 https://zhuanlan.zhihu.com/p/25436739

```python
class Solution(object):
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)==0:
            return 1
        if len(nums)==1:
            return 1 if nums[0]!=1 else 2
        i = 0
        while i<len(nums):
            if nums[i]>len(nums) or nums[i]<=0:
                nums[i] = 0
            elif nums[i]!=nums[nums[i]-1]:
                temp = nums[nums[i]-1]
                nums[nums[i]-1] = nums[i]
                nums[i] = temp
                i -= 1
            i += 1
        
        for i in range(len(nums)):
            if nums[i]!=i+1:
                return i+1
        return len(nums)+1
```

**类似题目：**

[Couples Holding Hands](https://leetcode.com/problems/couples-holding-hands/)