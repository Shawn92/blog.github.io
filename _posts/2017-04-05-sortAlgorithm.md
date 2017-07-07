---
layout: post
title:  "排序算法整理"
categories: 代码笔记
tags: 排序  
author: Shawn
---

* content
{:toc}

## 复杂度和稳定性分析

| 排序算法      | 最好         | 最坏       | 平均      | 辅助空间  |稳定性
| ------------- |:-------------| -----------| ----------|-----------|-----
| 冒泡排序      | `O(n)`       | `O(n^2)`   | `O(n^2)`   | `O(1)`    |稳定
| 直接选择排序  | `O(n^2)`     | `O(n^2)`   | `O(n^2)`   | `O(1)`    |稳定
| 直接插入排序  | `O(n)`       | `O(n^2)`   | `O(n^2)`   | `O(1)`    |稳定
| 希尔排序排序  | `O(n^1.3)`   | `O(n^2)`   | - | `O(1)`    |不稳定
| 堆排序        | `O(nlogn)`   | `O(nlogn)` | `O(nlogn)` | `O(1)`    |不稳定
| 归并排序      | `O(nlogn)`   | `O(nlogn)` | `O(nlogn)` | `O(n)`    |稳定
| 快速排序      | `O(nlogn)`   | `O(n^2)`   | `O(nlogn)` | `O(logn)~O(n)`    |不稳定




---------------------------------------------------------------
## 具体实现

### 直接插入排序（插入排序）

```cpp
//直接插入排序（插入排序）:时间复杂度O(n2)，最好O(n),最坏O(n2)
void Sort::DirectInsertSort(vector<int> &array) {
	int len = array.size(), i, j, temp;
	for (i = 1; i < len; i++)
	{
		temp = array[i];
		for (j = i; j > 0 && array[j - 1] > temp; j--)
		{
			array[j] = array[j - 1];
		}
		array[j] = temp;
	}
}
```

### 希尔排序排序（插入排序）

```cpp
//希尔排序（插入排序）:时间复杂度O(nlogn)，最好O(n),最坏O(n2)
void Sort::ShellSort(vector<int> &array) {
	int len = array.size(), i, j, temp, increment;
	for (increment = len / 2; increment > 0; increment /= 2)
	{
		for (i = increment; i < len; i++)
		{
			temp = array[i];
			for (j = i; j > increment && array[j - 1] > temp; j -= increment)
			{
				array[j] = array[j - increment];
			}
			array[j] = temp;
		}
	}
}
```

### 直接插入排序（插入排序）

```cpp
//直接选择排序（选择排序）:时间复杂度O(n2)，最好O(n2),最坏O(n2)
void Sort::DirectSelectSort(vector<int> &array) {
	int i, j, len = array.size(), min;
	
	for (i = 0; i < len; i++)
	{
		min = i;
		for (j = i; j < len; j++)
		{
			if (array[j] < array[min])
				min = j;
		}
		if (min != i)
		{
			array[i] = array[min] + array[i];
			array[min] = array[i] - array[min];
			array[i] = array[i] - array[min];
		}
	}
}
```

### 冒泡排序（交换排序）

```cpp

//冒泡排序（交换排序）:时间复杂度O(n2)，最好O(n),最坏O(n2)
void Sort::BubbleSort(vector<int> & array) {
	int i, j, len = array.size();
	int flag = 0;
	for (i = 0; i < len; i++)
	{
		flag = 0;
		for (j = 1; j < len - i; j++)
		{
			if (array[j] < array[j - 1]) {
				array[j] = array[j - 1] + array[j];
				array[j - 1] = array[j] - array[j - 1];
				array[j] = array[j] - array[j - 1];
				flag = 1;
			}
		}
		if (flag == 0) return;
	}
}
```

### 归并排序

```cpp
//归并排序:时间复杂度O(nlgn)，最好O(nlgn),最坏O(nlgn)
void Sort::Merge(vector<int>& array, int start, int mid, int end)
{
	vector<int> tempArray;
	int i = start, j = mid + 1;
	while (i <= mid  && j <= end)
	{
		if (array[i] < array[j]) {
			tempArray.push_back(array[i]);
			i++;
		}
		else{
			tempArray.push_back(array[j]);
			j++;
		}
	}
	while (i <= mid) {
		tempArray.push_back(array[i]);
		i++;
	}
	while (j <= end) {
		tempArray.push_back(array[j]);
		j++;
	}
	for (i = 0; i < tempArray.size(); ++i)
	{
		array[start + i] = tempArray[i];
	}
}

void Sort::MergeSort(vector<int> &array, int start, int end) {
	if (start < end){
		int mid = (start + end) / 2; //计算中间位置
		MergeSort(array, start, mid);
		MergeSort(array, mid + 1, end);
		Merge(array, start, mid, end);
	}
}
```

### 快速排序

```cpp
//快速排序
int Sort::Partition(vector<int>& array, int l, int r)
{
	int key = array[l];
	while (l < r)
	{
		while (l < r && array[r] > key){
			r--;
		}
		array[l] = array[r];

		while (l < r && array[l] < key){
			l++;
		}
		array[r] = array[l];
	}

	array[l] = key;
	return l;
}

//第二种分治方法
/* 
int Sort::Partition(vector<int>& array, int l, int r)
{
	//每次交换值之前，l和r同时移动
	int key = array[l], start = l;
	while (l < r)
	{
		while (l < r && array[l] <= key)
			l++;
		while (l < r && array[r] > key) 
			r--;

		if (l < r) {
			swap(array[r], array[l]);
			l++;
			r--;
		}
	}

	swap(array[r], array[start];
	return r;
}
*/

void Sort::QucikSort(vector<int>& array, int l, int r)
{
	if (l < r){
		int p = Partition(array, l, r);
		QucikSort(array, l, p - 1);
		QucikSort(array, p + 1, r);
	}
}

```
