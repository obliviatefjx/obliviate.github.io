---
title: 337. House Robber III
date: 2019-09-17 23:15:20
tags:
---

Medium

https://leetcode.com/problems/house-robber-iii/

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

**Example 1:**

```
Input: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

Output: 7 
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

---

2019.9.16 做出了一半吧，参考 https://www.cnblogs.com/grandyang/p/5275096.html

**方法：**

一开始用纯 DFS，超时。

后来先遍历节点，把每个节点都存在一个数组中，然后根据序号取节点，还是超时。

参考博客发现可以把节点存在字典里（我怎么没想到...！

于是一边遍历一边把遍历过的节点存在字典里，过了。

```python
class Solution(object):
    def rob(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        if not root.left and not root.right:
            return root.val
        money = {}
        dfs(root, money)
        return max(money[root])

def dfs(node, money):
    if not node:
        return
    if not node.left and not node.right:
        money[node] = (node.val, 0)
        return
    dfs(node.left, money)
    dfs(node.right, money)
    if not node.left:
        money[node] = (node.val+money[node.right][1], max(money[node.right]))
        return
    if not node.right:
        money[node] = (node.val+money[node.left][1], max(money[node.left]))
        return
    money[node] = (node.val+money[node.left][1]+money[node.right][1], max(money[node.left])+max(money[node.right]))
    return
```

**类似题目：**

[House Robber II](https://leetcode.com/problems/house-robber-ii/)

