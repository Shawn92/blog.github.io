---
layout: post
title:  "八皇后问题"
categories: 代码笔记
tags: 八皇后 全排列
author: Shawn
---

* content
{:toc}

## 八皇后问题

**题目描述：**略

**思路：**先计算出所有结果的全排列，然后判断全排列的结果是否符合








---------------------------------------------------------------
## 代码

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <unordered_set>
#include <algorithm>
using namespace std;
int NUM = 0;

//**********************全排列函数结束**********************
//递归函数，当前已排序了字符串str中的前（k-1）个字符，现在开始将第k个字符一次与后面的字符交换
void AllArrange(string str, int k, vector<string>& res) {
	if (k == str.size() - 1)
		res.push_back(str);
	unordered_set<char> us;// 记录已经交换过的字符
	sort(str.begin() + k, str.end());//保证按照字典续交换
	for (int i = k; i < str.size(); ++i) {
		//先于自身交换一次，这里不能改成从k+1开始交换，这样会少一类结果
		if (us.find(str[i]) == us.end()) {
			us.insert(str[i]);
			swap(str[k], str[i]);//如果没有找到的话，就交换一次
			AllArrange(str, k + 1, res);
			swap(str[k], str[i]);//回溯，还原字符串用于下一次交换
		}
	}
}

vector<string> AllArrange(string str) {
	vector<string> res;
	if (str.size() == 0)
		return res;
	//调用递归函数
	AllArrange(str, 0, res);
	return res;
}
//**********************全排列函数结束**********************

//************************打印函数**************************
void print(string str) {
	int checkerboard[8][8] = { 0 };
	for (int i = 0; i < 8; ++i)
			checkerboard[i][str[i]-'0'] = 1;
	
	cout << "正在打印第" << NUM+1 << "种解法" << endl;
	ofstream out("out.txt", ios::app);
	out << "----------第" << (++NUM) << "种解法：--------------" << endl;
	if (out.is_open()) {
		for (int i = 0; i < 8; ++i) {
			for (int j = 0; j < 8; ++j) {
				out << checkerboard[i][j] << ' ';
			}
			out << endl;
		}
	}
}

//********************判断棋盘是否合法**************************
//判断棋盘是否合法
bool Judge(string str) {
	for (int i = 0; i < 8; ++i) {
		for (int j = i+1; j < 8; ++j) {
			if ((i - j) == str[i] - str[j] || (j - i) == str[i] - str[j])
				return false;
		}
	}
	return true;

}

//构造棋盘
void JudgeuuQueen(vector<string> res) {
	for (int i = 0; i < res.size(); ++i) {
		if (Judge(res[i]))
			print(res[i]);
	}
}
 
int main() {
	
	string str = "01234567";
	vector<string> res;
	res = AllArrange(str);
	JudgeuuQueen(res);
	
	system("pause");

	return 0;
}
```
