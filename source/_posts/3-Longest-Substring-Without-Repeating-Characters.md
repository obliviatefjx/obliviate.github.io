---
title: 3. Longest Substring Without Repeating Characters
date: 2019-09-22 21:18:19
tags:
---

Medium

https://leetcode.com/problems/longest-substring-without-repeating-characters/

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

---

2019.9.22 做出来了

**方法：**

用一个字典 idx{} 记录截止到目前为止出现的字符的 index（如果出现了多次就保留最后一次出现的 index）。

用两个指针 i,j，i 和 j 之间的字符串是无重复字符的。

对于每个字符 s[j]，如果 s[j] 已经出现过（在字典里）且出现的位置大于等于 i（idx[s[j]]>=i），那么 s[j] 一定是在 s[i:j+1] 之间的字符串，这时就令 i = idx[s[j]]+1，把重复字符越过去。

每次都令 j += 1 来扩大右边界。

```python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        if len(s)<=1:
            return len(s)
        idx = {}
        i,j = 0,0
        ans = 0
        while j<len(s):
            if s[j] in idx and idx[s[j]]>=i:
                i = idx[s[j]]+1
            idx[s[j]] = j
            j += 1
            ans = max(ans, j-i)
        return ans
```

**类似题目：**

Longest Substring with At Most Two Distinct Characters
Longest Substring with At Most K Distinct Characters
Subarrays with K Different Integers