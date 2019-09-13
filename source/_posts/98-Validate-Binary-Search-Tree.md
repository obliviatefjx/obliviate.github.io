---
title: 98. Validate Binary Search Tree
date: 2019-09-10 23:51:30
tags:
---

Medium

https://leetcode.com/problems/validate-binary-search-tree/

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

```
    2
   / \
  1   3

Input: [2,1,3]
Output: true
```

---

2019.9.10 独立做出来了

**方法：**

DFS

DFS(node) 返回三个变量：以当前 node 为根的树的最小值、最大值、是否为 BST

```python
class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        _, _, ans = dfs(root)
        return ans
    
def dfs(node):
    if not node.left and not node.right:
        return node.val, node.val, True
    if node.left:
        l_min, l_max, l_ans = dfs(node.left)
        if not l_ans or l_max>=node.val:
            return l_min, l_max, False
    else:
        l_min = node.val
    if node.right:
        r_min, r_max, r_ans = dfs(node.right)
        if not r_ans or r_min<=node.val:
            return r_min, r_max, False
    else:
        r_max = node.val
    return l_min, r_max, True
```

**类似题目：**

Binary Tree Inorder Traversal
Find Mode in Binary Search Tree