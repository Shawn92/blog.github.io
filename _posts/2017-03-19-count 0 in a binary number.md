---
layout: post
title:  "统计二进制数中“1”的个数"
categories: JavaScript
tags:  C++ 编程
author: Dora
---

* content
{:toc}

## 问题

**问题描述：**世界上有10种人，一种懂二进制，一种不懂。那么你知道两个int32整数m和n的二进制表达，有多少个位(bit)不同么？ （小米2016年 ）

**函数原型：** `int countBitDiff(int m, int n)`

**输入：**
>1999 2299

**输出：**
>7





**解析：** 本题目来自2016年小米的在线笔试题，要比较`m`和`n`的二进制位的不同，可以借助额外的变量`v`以及异或操作来实现，做法是：

    v=m^n;
    
经过异或操作后`v`的二进制表示中的二进制数`1`的数量就是`m`和`n`的不同二进制位的个数，问题转化为求一个二进制数`v`中二进制数`1`的个数。

------------------------------

## 解法一：逐位比较

最容易想到的方法是将`v`中各个位上的二进制值逐一与`1`比较，《C和指针》中使用移位运算符实现了这样的比较：
```python
/**
 * 获得两个整形二进制表达位数不同的数量
 * @param m 整数m
 * @param n 整数n
 * @return 整型
 */
int countBitDiff(int m, int n) {
	unsigned int c = m ^ n; 
	char ones;
	for (ones = 0; c != 0; c >>= 1)
	{
		if ((c & 1) != 0)
			ones += 1;
	}
	return ones;
}
```    
## 解法二：借助n&(n-1)**

第二种方法比较特殊，用到了按位与特一个特殊性质，即：

>假设二进制数`n`中有`k`位上的二进制数是`1`,     
>那么`n&(n-1)`中二级制值为`1`的位数为`k-1`.

使用`n&(n-1)`的特殊性质，可以编写如下代码：
```cpp
/**
 * 获得两个整形二进制表达位数不同的数量
 * @param m 整数m
 * @param n 整数n
 * @return 整型
 */
int countBitDiff(int m, int n) {
	int c = m ^ n; //按位异或
	char counter = 0;
	for (; c; ++counter) c &= (c - 1);
	return counter;
}
```
