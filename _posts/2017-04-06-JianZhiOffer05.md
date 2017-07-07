---
layout: post
title:  "剑指Offer05：从尾到头打印链表"
categories: 代码笔记
tags: 剑指offer 链表 
author: Shawn
---

* content
{:toc}

## 从尾到头打印链表
**题目描述：**输入一个链表，从尾到头打印链表每个节点的值。



---------------------------------------------------------------
## 代码

```cpp
vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> res;
        std::stack<ListNode*> nodes;
        ListNode *p = head;
        while (p != NULL) {
            nodes.push(p);
            p = p->next;
        }
        
        while(!nodes.empty()) {
            p = nodes.top();
           	res.push_back(p->val);
            nodes.pop();
        }
		return res;
    }
}
```
