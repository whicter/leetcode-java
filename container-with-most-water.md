# 11. Container With Most Water

### 题目描述

>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

#### Example

[原题链接](https://leetcode.com/problems/container-with-most-water/description/)

### 解题思路
移动pointer条件：
- 左低右高移动左
- 左高右低移动右

###  Java代码实现

``` java
public class Solution {
    public int maxArea(int[] height) {
    	if (height == null || height.length < 2) {
    		return 0;
    	}
    
    	int left = 0, right = height.length - 1;
    	int max = 0;
    
    	while (left < right) {
    		max = Math.max(max, (right - left) * Math.min(height[left], height[right]));
    		if (height[left] < height[right]) {
    			left ++;
    		} else {
    			right --;
    		}
    	}
    	return max;
    }
}
```