---
title: 647. Palindromic Substrings
date: 2019-09-15 23:14:03
tags:
---

Medium

https://leetcode.com/problems/palindromic-substrings/

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**

```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

---

2019.9.15 知道用马拉车方法做，照抄的第 5 题的马拉车算法，但是没能自己写出马拉车算法。

**方法：**

马拉车算法好厉害！

注意 ans += p[i]/2 （而不是 ans += p[i]）

```python
class Solution(object):
    def countSubstrings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if len(s)<=1:
            return len(s)
        t = '@#'
        for c in s:
            t += c
            t += '#'
        p = [0]*len(t)
        ans = 0
        mx = 0
        idx = 0
        for i in range(1,len(t)):
            if mx>i:
                p[i] = min(p[2*idx-i], mx-i)
            else:
                p[i] = 1
            while i-p[i]>=0 and i+p[i]<len(t) and t[i+p[i]]==t[i-p[i]]:
                p[i] += 1
            if mx<i+p[i]:
                mx = i + p[i]
                idx = i
            ans += p[i]/2
        return ans
```

**类似题目：**

Longest Palindromic Substring
Longest Palindromic Subsequence
Palindromic Substrings