---
title: 621. Task Scheduler
date: 2019-09-02 23:41:08
tags:
---

Medium

https://leetcode.com/problems/task-scheduler/

Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks. Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval **n** that means between two **same tasks**, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the **least** number of intervals the CPU will take to finish all the given tasks.

**Example:**

```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```

**Note:**

1. The number of tasks is in the range [1, 10000].
2. The integer n is in the range [0, 100].

------

2019.9.2 没做出来，参考 https://www.cnblogs.com/grandyang/p/7098764.html

**方法：**

首先统计 task[] 中次数最多的 task **M** 的次数 maxTask，然后找出现次数最多的 task 的个数 maxTime。

每隔 n 个 timestep 就放一个 task **M**，然后其它的 task 填充在间隔里，不足的补 idle，这样一共有 (n+1)*(maxTask-1) 个 timestep，最后还有个小尾巴是剩下的次数最多的 task 的个数 maxTime。

返回结果时需要和 len(tasks) 比较后取 max 是因为可能各 task 数都比较平均，不用填 idle，反而还多出来了 task。所用时间至少应为 len(tasks)。

```python
class Solution(object):
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        cnt = {}
        maxTask = 0
        for t in tasks:
            cnt[t] = cnt.get(t,0) + 1
            maxTask = max(maxTask, cnt[t])
        maxTime = 0
        for t in cnt:
            if cnt[t]==maxTask:
                maxTime += 1
        return max(len(tasks), (n+1)*(maxTask-1)+maxTime)
```



**类似题目：**

Rearrange String k Distance Apart
Reorganize String