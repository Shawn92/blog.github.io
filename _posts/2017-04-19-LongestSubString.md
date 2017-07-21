---
layout: post
title:  "最长子序列问题"
categories: 代码笔记
tags: 动态规划 子序列
author: Shawn
---

* content
{:toc}

## 最长子序列问题

**题目描述：求一个无需序列的最长公共子序列

**思路：**使用动态规划求解








---------------------------------------------------------------
## 代码

```cpp
#include <iostream>
#include <vector>
using namespace std;

int lis(int arr[], int len) {
	int* lis = (int*)malloc(sizeof(int) * len);//lis[i] 中保存的师到arr[i]为止，最长递增子序列的长度
	for (int i = 0; i < len; ++i)
		lis[i] = 1;

	for (int i = 1; i < len; i++)              //动态规划函数，每次将arr[i]与arr[0]-arr[i-1]比较，同步更新当前的lis[i]
		for (int j = 0; j < i - 1; ++j) 
			if (arr[i] > arr[j] && lis[i] < lis[j] + 1)
				lis[i] = lis[j] + 1;
	
	int max = 0;

	for (int i = 0; i < len; ++i)
		if (lis[i] > max)
			max = lis[i];

	free(lis);

	return max;;
}

int main() {
	int arr[] = { 3,1,4,1,5,9,2,6,5 };
	cout << lis(arr, 9) << endl;
	system("pause");
	return 0;
}
```
