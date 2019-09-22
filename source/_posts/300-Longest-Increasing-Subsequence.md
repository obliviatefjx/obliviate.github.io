---
title: 300. Longest Increasing Subsequence
date: 2019-09-22 17:16:14
tags:
---

Medium

https://leetcode.com/problems/longest-increasing-subsequence/

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:**

- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?

---

2019.9.21 没做出来，参考 https://blog.csdn.net/chaochen1407/article/details/82833885

**方法：**

用一个长度为 len(nums) 的数组 seqs[] 记录，seqs[k] 表示长度为 k+1 的递增序列的尾元素值。并用一个变量 max_len 表示当前递增子序列的最大长度。

遍历 nums[] 中的元素，对于新来的元素 n 来说：

​	1）若 n<seqs[0]，则 n 小于长度为 1 的递增子序列，也就是 n 是目前为止最小的值，更新 seqs[0]=n。

​	2）若 n>seqs[max_len-1]，则 n 比当前的最长递增子序列的尾元素还大，说明 n 可以加在其后，形成 max_len+1 的递增子序列。因此令 seqs[max_len] = n，同时 max_len 加 1。

​	3）若不满足条件 1 和 2，则需要在长度为 1~max_len 的递增子序列中找到一个尾元素值刚好大于等于 n 的序列，把那个序列的尾元素值更新为 n，因为这样的话之后的元素值就更可能加在队列里形成递增子序列。采用二分查找的方法找那个序列。

时间复杂度 O(nlogn)

```python
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)<=1:
            return len(nums)
        max_len = 1
        seqs = [float('inf')]*len(nums)
        for n in nums:
            if n<seqs[0]:
                seqs[0] = n
            elif n>seqs[max_len-1]:
                seqs[max_len] = n
                max_len += 1
            else:
                l,r = 0,max_len
                while l<r:
                    mid = l+(r-l)/2
                    if n>seqs[mid]:
                        l = mid+1
                    else:
                        r = mid
                seqs[l] = n
        return max_len
```

**类似题目：**

Increasing Triplet Subsequence
Russian Doll Envelopes
Maximum Length of Pair Chain
Number of Longest Increasing Subsequence
Minimum ASCII Delete Sum for Two Strings