---
title: 124. Binary Tree Maximum Path Sum
date: 2019-09-10 01:03:25
tags:
---

Hard

https://leetcode.com/problems/binary-tree-maximum-path-sum/

Given a **non-empty** binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node** and does not need to go through the root.

**Example 1:**

```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

---

2019.9.10 独立做出来了

**方法：**

DFS

dfs(node) 函数里完成两个功能：

1. 计算 node.val + {左子树的最大路径值} + {右子树的最大路径值}，并和一个全局变量 ans 比较，令 ans 等于较大值。这样对每个 node 都计算一遍后就能得到树中的最大路径长了（不一定包含根节点）
2. 返回包含当前 node 的最大路径值，这个值需要确保大于等于 0 的。

和 https://www.cnblogs.com/grandyang/p/4280120.html 方法类似，只不过那个博主是在调用 dfs 之后取大于等于 0 的值，我是在调用 dfs 时就确保返回的一定是大于等于 0 的值，作用相同。

```python
 class Solution(object):
    def maxPathSum(self, root):
        """ 
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        self.ans = -float('inf')
        self.dfs(root)
        return self.ans
        
    def dfs(self, node):
        if not node:
            return 0
        if not node.left and not node.right:
            self.ans = max(self.ans, node.val)
            return max(node.val,0)
        left = self.dfs(node.left)
        right = self.dfs(node.right)
        self.ans = max(self.ans, node.val+left+right)
        return max(max(left, right)+node.val, 0)
```

**类似题目：**

Path Sum
Sum Root to Leaf Numbers
Path Sum IV
Longest Univalue Path