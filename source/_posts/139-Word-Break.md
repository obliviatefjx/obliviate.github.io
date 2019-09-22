---
title: 139. Word Break
date: 2019-09-22 20:22:49
tags:
---

Medium

https://leetcode.com/problems/word-break/

Given a **non-empty** string *s* and a dictionary *wordDict* containing a list of **non-empty** words, determine if *s* can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

---

2019.9.22 没做出来，参考 https://blog.csdn.net/fuxuemingzhu/article/details/79368360

一开始用了 DFS 做，能过一部分但是还是会超时。

这题我真是万万没想到用 DP 做...曾经有过一闪念，但是觉得没法做就没接着想了。

**方法：**

思路：如果 s 能被拆分，则存在 s[:i] 能被拆分且 s[i:] 在字典中。因此得到 s[:i] 与 s 的递推关系式。

新建一个长度为 len(s)+1 的数组 dp[]，其中 dp[i] 表示字符串 s[:i] 能否被拆分。

初始化 dp[0] = True。

采用两重循环，外层循环中的 i 是待判断的 dp[i] 的 index，然后在内层循环里用 j 遍历 0~i-1 来分别尝试拆分 s[:i]。

```python
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        if len(wordDict)==0:
            return False
        dp = [False]*(len(s)+1)
        dp[0] = True
        for i in range(1, len(s)+1):
            for j in range(i):
                if dp[j] and s[j:i] in wordDict:
                    dp[i] = True
        return dp[-1]
```

**类似题目：**

[Word Break II](https://leetcode.com/problems/word-break-ii/)

