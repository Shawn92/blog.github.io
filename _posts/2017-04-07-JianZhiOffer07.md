---
layout: post
title:  "剑指Offer07：用两个栈实现队列"
categories: 代码笔记
tags: 剑指offer 栈 队列 stack deque
author: Shawn
---

* content
{:toc}

## 用两个栈实现队列
**题目描述：**用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。



---------------------------------------------------------------
## 代码

```cpp
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }

    int pop() {
        if (stack2.size() <= 0) {
            while (stack1.size() > 0) {
                int top = stack1.top();
                stack1.pop();
                stack2.push(top);
            }
        }
        
        int res = stack2.top();
        stack2.pop();
        return res;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
```
