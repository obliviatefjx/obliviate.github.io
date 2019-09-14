---
title: 4. Median of Two Sorted Arrays
date: 2019-09-14 19:26:06
tags:
---

Hard

https://leetcode.com/problems/median-of-two-sorted-arrays/

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume **nums1** and **nums2** cannot be both empty.

**Example 1:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

---

2019.9.14 没做出来，参考 https://www.cnblogs.com/zuoyuan/p/3759682.html、https://www.cnblogs.com/grandyang/p/4465932.html

**方法：**

想到了用二分查找，但是没想到是**对 k 二分**。

这道题的关键是把 **“找 nums1 与 nums2 的中位数”** 的问题转化为用一个 getKth(nums1, nums2, k) 函数 **“找 nums1 与 nums2 中第 k (1<=k<=len(nums1)+len(nums2)) 大的数"**（当然我没想到 _\(:з」∠)\_

1. 对于 getKth(nums1, nums2, k)，需要确保 len(nums1)<=len(nums2)，若不满足的话则 return getKth(nums2, nums1, k)
2. 由于上一条确保了 len(nums1)<=len(nums2)，所以如果 len(nums1)==0 的话则直接返回 nums2[k-1]。
3. 如果 len(nums1) 与 len(nums2) 都大于 0 且 k==1，那么返回 min(nums1[0], nums2[0])。

（接下来是重头戏：对 k 二分）

4. 比较 nums1[k/2-1] 与 nums2[k/2-1] 的大小：

   1）如果 nums1[k/2-1] <= nums2[k/2-1]，那么 **nums1[k/2-1]** 在 nums1 中是第 k/2 大的数，同时在 nums2 中最多是第 k/2 -1 大的数（因为 nums1[k/2-1] 小于 nums2 中第 k/2 大的数：nums2[k/2-1]），所以 nums1[k/2-1] 在 nums1 与 nums2 的总数组中**最多是第 (k/2 + k/2 -1) = k-1 大的数**，所以 nums1 与 nums2 中第 k 大的数必然不在 nums1[:k/2] 中，因此可以继续从 nums1[k/2:] 与 nums2 中找第 k/2 大的数。

   2）如果 nums1[k/2-1] > nums2[k/2-1]，与1) 同理，继续从 nums1 与 nums2[k/2:] 中找第 k/2 大的数。

```python
class Solution(object):
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        len1, len2 = len(nums1), len(nums2)
        if (len1+len2)%2==1:
            return getKth(nums1, nums2, (len1+len2+1)/2)
        else:
            return (getKth(nums1, nums2, (len1+len2+1)/2) + getKth(nums1, nums2, (len1+len2+2)/2)) / 2.0
        
def getKth(nums1, nums2, k):
    len1, len2 = len(nums1), len(nums2)
    if len1>len2:
        return getKth(nums2, nums1, k)
    if len1==0:
        return nums2[k-1]
    if k==1:
        return min(nums1[0], nums2[0])
    p1 = min(k/2, len1)
    p2 = k - p1
    if nums1[p1-1] <= nums2[p2-1]:
        return getKth(nums1[p1:], nums2, p2)
    else:
        return getKth(nums1, nums2[p2:], p1)
```

**类似题目：**

The Skyline Problem
Maximum Swap
Find K-th Smallest Pair Distance