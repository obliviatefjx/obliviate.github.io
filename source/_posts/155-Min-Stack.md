---
title: 155. Min Stack
date: 2019-09-13 17:53:11
tags:
---

Easy

https://leetcode.com/problems/min-stack/

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack. 

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

---

2019.9.13 没做出来，参考 https://blog.csdn.net/fuxuemingzhu/article/details/79253237

**方法：**

辅助栈

将新增数字 append 到 stack[] 末尾，并将当前的最小值 append 到辅助栈 min[] 末尾，pop 的时候同时将两个栈的末尾元素出栈。

```python
class MinStack(object):
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []
        self.min = []
        
    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        self.stack.append(x)
        if len(self.min)==0:
            self.min.append(x)
        else:
            self.min.append(min(x, self.min[-1]))
        
    def pop(self):
        """
        :rtype: None
        """
        self.stack.pop(-1)
        self.min.pop(-1)
        
    def top(self):
        """
        :rtype: int
        """
        return self.stack[-1]

    def getMin(self):
        """
        :rtype: int
        """
        return self.min[-1]
```

**类似题目：**

[Max Stack](https://leetcode.com/problems/max-stack/)

