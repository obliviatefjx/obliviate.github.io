---
title: 287. Find the Duplicate Number
date: 2019-08-30 22:04:13
tags:
---

Medium

https://leetcode.com/problems/find-the-duplicate-number/

Given an array *nums* containing *n* + 1 integers where each integer is between 1 and *n* (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Example 1:**

```
Input: [1,3,4,2,2]
Output: 2
```

**Note:**

1. You **must not** modify the array (assume the array is read only).
2. You must use only constant, *O*(1) extra space.
3. Your runtime complexity should be less than *O*(*n*2).
4. There is only one duplicate number in the array, but it could be repeated more than once.

------------

2019.8.30 没做出来，参考 https://blog.csdn.net/fuxuemingzhu/article/details/79530847

题目本身不难，加上限制条件之后好难鸭。

像这种 “Given an array *nums* containing *n* + 1 (或 *n*) integer” 又 “each integer is between 1 and *n*” 的题就想到把元素值和位置做关联。但是想半天没想出答案。

**方法一：**

参考 http://bookshadow.com/weblog/2015/09/28/leetcode-find-duplicate-number/

把问题转换为有环链表的找环入口的问题。

每访问一个元素 n，就跳转到 nums[n] 来访问新的元素，循环往复。如果数组 nums[] 中没有重复值的话，那么每个位置都最多只会被访问 1 次，因此如果有元素被访问了两次，那么该元素在 nums[] 中的 index 就是 nums[] 中的重复值。

可以把 nums[i] 的值看作一个 ListNode，ListNode.val = nums[i] 表示 ListNode.next 的 “地址”，这样寻找 nums[] 的重复值就变为了找链表中一个重复的地址，即有环链表中的环入口。

时间复杂度 O(n)，空间复杂度 O(1)。

注意：最后返回的是 index 而不是 nums[index]

```python
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        slow, fast = 0, 0
        while True:
            fast = nums[nums[fast]]
            slow = nums[slow]
            if slow==fast:
                fast = 0
                while slow!=fast:
                    fast = nums[fast]
                    slow = nums[slow]
                return slow
```

上面的代码是我自己写的，太丑了...看了别人的写法改成了下面的，看着舒服多了。

```python
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        slow = nums[0]
        fast = nums[nums[0]]
        while slow!=fast:
            fast = nums[nums[fast]]
            slow = nums[slow]
        fast = 0
        while slow!=fast:
            fast = nums[fast]
            slow = nums[slow]
        return slow
```



**方法二：**

"二分枚举答案范围，使用鸽笼原理进行检验，根据鸽笼原理，给定 n+1 个范围 [1, n] 的整数，其中一定存在数字出现至少两次。

假设枚举的数字为 n / 2：

遍历数组，若数组中不大于 n / 2 的数字个数超过 n / 2 ，则可以确定 [1, n /2] 范围内一定有解，否则可以确定解落在 (n / 2, n] 范围内。"

看了上述讲解后明白了，写的代码还是没过，二分查找的边界条件好难确定啊，最后照着答案打的通过了。

```python
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        l,r = 1,len(nums)-1
        while l<=r:
            cnt = 0
            mid = l + (r - l) / 2
            for n in nums:
                if n<=mid:
                    cnt += 1
            if cnt>mid:
                r = mid-1
            else:
                l = mid+1
        return l
```



**类似题目：**

First Missing Positive
Missing Number
Set Mismatch