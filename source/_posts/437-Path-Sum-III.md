---
title: 437. Path Sum III
date: 2019-09-13 17:37:59
tags:
---

Easy

https://leetcode.com/problems/path-sum-iii/

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

**Example:**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

---

2019.9.13 没做出来，参考 https://blog.csdn.net/fuxuemingzhu/article/details/71097135

**方法：**

DFS + DFS（一个 DFS 本身会调用自己，同时也调用另一个 DFS）

```python
class Solution(object):
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: int
        """
        if not root:
            return 0
        return dfs(root, sum) + self.pathSum(root.left, sum) + self.pathSum(root.right, sum)

def dfs(node, cur):
    if not node:
        return 0
    ans = 0
    if cur==node.val:
        ans += 1
    ans += dfs(node.left, cur-node.val)
    ans += dfs(node.right, cur-node.val)
    return ans
```

**类似题目：**

Path Sum
Path Sum II
Path Sum IV
Longest Univalue Path

