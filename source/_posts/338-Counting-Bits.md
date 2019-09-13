---
title: 338. Counting Bits
date: 2019-09-12 00:58:19
tags:
---

Medium

https://leetcode.com/problems/counting-bits/

Given a non negative integer number **num**. For every numbers **i** in the range **0 ≤ i ≤ num** calculate the number of 1's in their binary representation and return them as an array.

**Example 1:**

```
Input: 2
Output: [0,1,1]
```

**Follow up:**

- It is very easy to come up with a solution with run time **O(n\*sizeof(integer))**. But can you do it in linear time **O(n)** /possibly in a single pass?
- Space complexity should be **O(n)**.
- Can you do it like a boss? Do it without using any builtin function like **__builtin_popcount** in c++ or in any other language.

---

2019.9.12 独立做出来了

**方法：**

DP + 位运算

对于一个数 n 来说，**n&(n-1) 可以把 n 的二进制表示上的最后一个 ‘1’ 删除**。

因此 n 的二进制表示中 ‘1’ 的个数 = n&(n-1) 的二进制表示中 ‘1’ 的个数 + 1，由此写 DP。

```python
class Solution(object):
    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """
        if num==0:
            return [0]
        ans = [0]*(num+1)
        for i in range(1, num+1):
            temp = i&(i-1)
            if temp==0:
                ans[i] = 1
            else:
                ans[i] = ans[temp]+1
        return ans
```

**类似题目：**

[Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

