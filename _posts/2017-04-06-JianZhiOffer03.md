---
layout: post
title:  "剑指Offer03：二维数组中的查找"
categories: 代码笔记
tags: 剑指offer 二维数组 查找 
author: Shawn
---

* content
{:toc}

## 二维数组中的查找
**题目描述：** 在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。



---------------------------------------------------------------
## 代码

```cpp
//思想：从左上或者右下开始查找
bool Find(int target, vector<vector<int> > array) {
	if (array.size() == 0)
		return false;
	int i = 0;
	int j = array[0].size() - 1;

	while (i < array.size() && j >= 0) {
		if (array[i][j] == target)
			return true;
		else if (array[i][j] > target)
			--j;
		else
			++i;
	}
	return false;
}
```
