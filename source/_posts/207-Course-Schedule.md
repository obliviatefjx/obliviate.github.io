---
title: 207. Course Schedule
date: 2019-09-22 17:58:11
tags:
---

Medium

https://leetcode.com/problems/course-schedule/

There are a total of *n* courses you have to take, labeled from `0` to `n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?

**Example 1:**

```
Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```

**Note:**

1. The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

---

2019.9.22 做出来了

其实严格来说不算是独立做出来的，因为昨天正好有一个笔试题是有向图的拓扑排序，所以才能写出来，参考了 

https://blog.csdn.net/lanchunhui/article/details/50957608

**方法：**

有向图的拓扑排序

注意构建有向图时，字典的 key 是有向图箭头的起始点，value 是箭头的终点，也就是说 key 是前提，value 是依赖 key 的。

```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        if numCourses==0 or len(prerequisites)<=1:
            return True
        G = dict((i,[]) for i in range(numCourses))
        for p,q in prerequisites:
            G[q].append(p)
        ans = topSort(G)
        return True if len(ans)==numCourses else False

def topSort(G):
    in_degree = dict((u,0) for u in G)
    for u in G:
        for v in G[u]:
            in_degree[v] += 1
    
    Q = [u for u in G if in_degree[u]==0]
    S = []
    while Q:
        u = Q.pop()
        S.append(u)
        for v in G[u]:
            in_degree[v] -= 1
            if in_degree[v]==0:
                Q.append(v)
    return S
```

**类似题目：**

Course Schedule II
Graph Valid Tree
Minimum Height Trees
Course Schedule III