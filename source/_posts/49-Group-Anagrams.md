---
title: 49. Group Anagrams
date: 2019-09-16 00:30:28
tags:
---

Medium

https://leetcode.com/problems/group-anagrams/

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

- All inputs will be in lowercase.
- The order of your output does not matter

---

2019.9.15 独立做出来了（感觉我现在总想一蹴而就地写出最优解，但往往想不出来...就迟迟不写，要改正鸭

虽然做出来了，但是这道题之前应该是参考别人的方法提交过，Runtime = 76 ms, Memory = 15.8 MB，但是我没印象了，就自己想的方法。

以下三种方法从方法一到方法三依次做了速度优化。

**方法一：**

由于题目限定了字符串都是小写英文字母，因此可以把字符映射到长为 26 的数字串中，数字串每位对应相应小写字母的个数。把这个数字串作为 key 用于字典中，value 为数字串为 key 的字符串数组。

（很慢）Runtime = 236 ms, Memory = 15.1 MB

```python
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        if len(strs)==0:
            return []
        if len(strs)==1:
            return [strs]
        ans = {}
        for s in strs:
            num = str2num(s)
            if num not in ans:
                ans[num] = [s]
            else:
                ans[num].append(s)
        return ans.values()
        
def str2num(s):
    cnt = {}
    for c in s:
        cnt[c] = cnt.get(c, 0) + 1
    ans = ''
    for i in range(26):
        ans += str(cnt.get(chr(ord('a')+i), 0))
    return ans
```

**方法二：**

同样的思想，但是把 str2num() 函数改为了由字符串转换为字符升序的字符串（即标准字符串）函数，这样不用每次都统计 26 个字母。

（稍快）Runtime = 112 ms, Memory = 15.1 MB

```python
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        if len(strs)==0:
            return []
        if len(strs)==1:
            return [strs]
        ans = {}
        for s in strs:
            num = sort_str(s)
            if num not in ans:
                ans[num] = [s]
            else:
                ans[num].append(s)
        return ans.values()
        
def sort_str(s):
    num = sorted(map(ord, s))
    num = map(chr, num)
    ans = ''.join(num)
    return ans
```

**方法三：**

思路和方法二完全一样，只是修改了 sort_str() 函数里对字符串中字符排序的代码，直接对字符排序，而不用先映射到 ASCII 码再映射回来。

常规写法：**对字符串 s 中字符排序：ans = ''.join(sorted(list(s)))**

（最快）Runtime = 84 ms, Memory = 15.5 MB

```python
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        if len(strs)==0:
            return []
        if len(strs)==1:
            return [strs]
        ans = {}
        for s in strs:
            num = sort_str(s)
            if num not in ans:
                ans[num] = [s]
            else:
                ans[num].append(s)
        return ans.values()
        
def sort_str(s):
    num = sorted(list(s))
    ans = ''.join(num)
    return ans
```



**类似题目：**

Valid Anagram
Group Shifted Strings