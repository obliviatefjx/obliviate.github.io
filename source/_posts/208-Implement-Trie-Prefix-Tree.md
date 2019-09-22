---
title: 208. Implement Trie (Prefix Tree)
date: 2019-09-22 17:39:46
tags:
---

Medium

https://leetcode.com/problems/implement-trie-prefix-tree/

Implement a trie with `insert`, `search`, and `startsWith` methods.

**Example:**

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

**Note:**

- You may assume that all inputs are consist of lowercase letters `a-z`.
- All inputs are guaranteed to be non-empty strings.

---

2019.9.22 做出来了，正好前两天笔试考到了字典树

**方法：**

说是树，但是每个“节点”没有明显的左右儿子啥的，每个节点就是一个字典，字典的 key 是字母，对应的 value 也是字典（表示下一个字母），同时如果在该节点为止时形成了一个单词，那么需要在该节点的字典中加入一个终止符 self.end=-1。

```python
class Trie(object):
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = {}
        self.end = -1

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: None
        """
        cur = self.root
        for c in word:
            if c not in cur:
                cur[c] = {}
            cur = cur[c]
        cur[self.end] = True
        return

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        cur = self.root
        for c in word:
            if c not in cur:
                return False
            cur = cur[c]
        if self.end not in cur:
            return False
        return True   

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        cur = self.root
        for c in prefix:
            if c not in cur:
                return False
            cur = cur[c]
        return True          
```

**类似题目：**

Add and Search Word - Data structure design
Design Search Autocomplete System
Replace Words
Implement Magic Dictionary