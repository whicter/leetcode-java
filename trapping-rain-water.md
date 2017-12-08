# 42. Trapping Rain Water

### 题目描述

>Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

>For example, 
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.
#### Example

[原题链接](https://leetcode.com/problems/container-with-most-water/description/)

### 解题思路
移动pointer条件：
- 左低右高移动左
- 左高右低移动右

理由：
假设hL < hR, 储水量为hL * (R - L)
假如hR --, 获得的新高度为hR'
- 如果hR' < hL, 新的结果为: hR' * (R' - L);
- 如果hR' > hL, 新的结果为: hL * (R' - L);

无论哪个结果都不会带来更大的储水量，因此应该操作hL ++来找寻新的可能

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