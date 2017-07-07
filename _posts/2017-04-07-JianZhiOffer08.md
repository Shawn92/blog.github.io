---
layout: post
title:  "剑指Offer08：旋转数组的最小数字"
categories: 代码笔记
tags: 剑指offer 数组
author: Shawn
---

* content
{:toc}

## 旋转数组的最小数字
**题目描述：**把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。



---------------------------------------------------------------
## 代码

```cpp
class Solution {
public:
    int minNumberInRotateArray(vector<int> rotateArray) {
        int left = 0, right = rotateArray.size() - 1;
        int middle = left;
        while (rotateArray[left] >= rotateArray[right]) {
			if (right - left == 1) {
				middle = right;
                break;
            }
            
            middle = (right-left)/2+left;
            
            if (rotateArray[left] == rotateArray[middle] && 
                rotateArray[middle] == rotateArray[right]) {
                return findMin(rotateArray, left, right);
            }
            if (rotateArray[middle] >= rotateArray[left]) 
                left = middle;
            else if (rotateArray[middle] <= rotateArray[right])
                right = middle;
			
		}
		return rotateArray[middle];
    }
	
	//如果left等于right，需要单独处理
	int findMin(vector<int> rotateArray, int left, int right) {
		int min = rotateArray[left];
		for (int i = left+1; i <= right; ++i) {
			if(rotateArray[i] <= min)
				min = rotateArray[i];
		}
		return min;
	}
};
```
