---
layout: post
title:  "使用多重指针实现单链表的插入操作"
categories: 代码笔记
tags: 指针 链表 
author: Dora
---

* content
{:toc}
使用多重指针可以实现单向链表的快速插入和删除操作










```cpp
typedef struct NODE{
	int value;
	struct NODE *next;
} Node;

sll_insert(register Node **linkp, int new_valude)
{
	register Node *current;
	register Node *new;
	while((current = *linkp) != NULL && current->value < new_valude)
	{
		linkp = current->next;
	}
	
	new = (Node *)malloc(sizeof(Node));
	new-> = new_valude;
	new->next = current;
	*linkp = new;
	return true;
}
```
