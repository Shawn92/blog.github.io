---
layout: post
title:  "剑指Offer09：求斐波那契（尾递归法）"
categories: 代码笔记
tags: 剑指offer 数组
author: Shawn
---

* content
{:toc}

## 求斐波那契（尾递归法）
**题目描述：**大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项。






---------------------------------------------------------------
## 代码

```cpp
class Solution {
public:
	int Fibonacci(int n) {
		if (n <= 0) return 0;
		if (n == 1) return 1;
		else return FibonacciPro(n - 2, 0, 1);
	}

	int FibonacciPro(int left, int prePre, int pre) {
		if (left == 0) return prePre + pre;
		else return FibonacciPro(left - 1, pre, prePre + pre);
	}
};
```

## 变体一：青蛙上跳问题
**题目描述：**一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。


---------------------------------------------------------------
## 代码

```cpp
class Solution {
public:
    int jumpFloor(int number) {
		if (number <= 1) return 1;
		if (number == 2) return 2;
		else return FibonacciPro(number - 2, 1, 2);
	}

	int FibonacciPro(int left, int prePre, int pre) {
		if (left == 1) return prePre + pre;
		else return FibonacciPro(left - 1, pre, prePre + pre);
	}
};
```

## 变体二：填充问题
**题目描述：**我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？


---------------------------------------------------------------
## 代码

```cpp
class Solution {
public:
    int rectCover(int number) {
		if (number == 0) return 0;
        else if (number == 1) return 1;
    	else return FibonacciPro(number - 2, 1, 1);
	}

	int FibonacciPro(int left, int prePre, int pre) {
		if (left == 0) return prePre + pre;
		else return FibonacciPro(left - 1, pre, prePre + pre);
	}
};
```
