---
title: 5. Longest Palindromic Substring
date: 2019-09-12 22:59:49
tags:
---

Medium

https://leetcode.com/problems/longest-palindromic-substring/

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example 1:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

---

2019.9.12 没做出来，参考 https://blog.csdn.net/dyx404514/article/details/42061017（讲解）、https://www.cnblogs.com/grandyang/p/4475985.html （部分代码）、https://blog.csdn.net/qxqxqzzz/article/details/84800939（python 部分代码）

**方法：**

虽然暴力解法可以做出来，但是 O(n^2) 的复杂度很高。

**马拉车算法**可以用 O(n) 的时间复杂度解这道题：

1. 首先把输入字符串 s 的每个字符之间加一个 '#'，并在最前面加一个 '@' 以防越界，得到新字符串 t。
2. 新建数组 p[]，len(p) = len(t)，p[i] 表示以 t[i] 为中点的回文字符串的最大半径（包含 t[i]）。
3. 从左往右依次计算 p[i]。当计算 p[i]时，p[j]\(0<=j<i) 已经计算完毕。设 mx 为之前计算中最长回文子串的右端点的最大值，并且设取得这个最大值的位置为 idx。

（以下引用自 https://blog.csdn.net/dyx404514/article/details/42061017）

> （2）Len数组的计算
> 首先从左往右依次计算Len[i]，当计算Len[i]时，Len[j](0<=j<i)已经计算完毕。设P为之前计算中最长回文子串的右端点的最大值，并且设取得这个最大值的位置为po，分两种情况：
>
> 第一种情况：i<=P
>
> 那么找到i相对于po的对称位置，设为j，那么如果Len[j]<P-i，如下图：
>
> <img src="https://img-blog.csdn.net/20141221160212654" alt="img" style="zoom:50%;" />
>
>
> 那么说明以j为中心的回文串一定在以po为中心的回文串的内部，且j和i关于位置po对称，由回文串的定义可知，一个回文串反过来还是一个回文串，所以以i为中心的回文串的长度至少和以j为中心的回文串一样，即Len[i]>=Len[j]。因为Len[j]<P-i,所以说i+Len[j]<P。由对称性可知Len[i]=Len[j]。
>
> 如果Len[j]>=P-i,由对称性，说明以i为中心的回文串可能会延伸到P之外，而大于P的部分我们还没有进行匹配，所以要从P+1位置开始一个一个进行匹配，直到发生失配，从而更新P和对应的po以及Len[i]。
>
> <img src="https://img-blog.csdn.net/20141221160232375" alt="img" style="zoom:50%;" />
>
>
> 第二种情况: i>P
>
> 如果i比P还要大，说明对于中点为i的回文串还一点都没有匹配，这个时候，就只能老老实实地一个一个匹配了，匹配完成后要更新P的位置和对应的po以及Len[i]。
>
> <img src="https://img-blog.csdn.net/20141221160247614" alt="img" style="zoom:50%;" />

```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        if len(s)<=1:
            return s
        t = '@#'
        for c in s:
            t += c
            t += '#'
        p = [0]*len(t)
        mx = 0
        idx = 0
        ans_len = 0
        ans_center = 0

        for i in range(1, len(t)):
            if mx>i:
                p[i] = min(mx-i, p[2*idx-i])
            else:
                p[i] = 1
            while i-p[i]>=0 and i+p[i]<len(t) and t[i+p[i]]==t[i-p[i]]:
                p[i] += 1
            if mx<i+p[i]:
                mx = i + p[i]
                idx = i
            if p[i]>ans_len:
                ans_len = p[i]
                ans_center = i
        ans = t[ans_center-ans_len+1:ans_center+ans_len]
        return ans.replace('#', '')
```

**类似题目：**

Shortest Palindrome
Palindrome Permutation
Palindrome Pairs
Longest Palindromic Subsequence