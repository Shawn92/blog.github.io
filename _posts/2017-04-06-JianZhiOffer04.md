---
layout: post
title:  "剑指Offer04：替换空格"
categories: 代码笔记
tags: 剑指offer 字符串 
author: Shawn
---

* content
{:toc}

## 替换空格
**题目描述：**请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。



---------------------------------------------------------------
## 代码

```cpp
\\从后向前替换，先计算出替换后的字符串的长度
void replaceSpace(char *str, int length) {
	int replaceNum = 0;
	for (int i = 0; i < length; ++i)
		if (*(str + i) == ' ') 
			++replaceNum;

	int newIndex = length + 2 * replaceNum;     //新长度
	char *index = str + length; //当前str最后一位

	while (index >= str)
	{
		if (*index == ' ')
		{
			str[newIndex--] = '0';
			str[newIndex--] = '2';
			str[newIndex--] = '%';
		}
		else {
			str[newIndex--] = *index;
		}
		index--;
	}
}
```
