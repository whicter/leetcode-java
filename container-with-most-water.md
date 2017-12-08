# 11. Container With Most Water

### 题目描述

>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

#### Example

[原题链接](https://leetcode.com/problems/container-with-most-water/description/)

### 解题思路
From [Code Ganker](http://blog.csdn.net/linhuanmars/article/details/24063271)
这道题属于纯粹的字符串操作，要把一串单词安排成多行限定长度的字符串。主要难点在于空格的安排。
- 首先每个单词之间必须有空格隔开，而当当前行放不下更多的单词并且字符又不能填满长度L时，我们要把空格均匀的填充在单词之间。
- 如果剩余的空格量刚好是间隔倍数那么就均匀分配即可，否则还必须把多的一个空格放到前面的间隔里面。

实现中我们维护一个count计数记录当前长度，超过之后我们计算共同的空格量以及多出一个的空格量，然后将当行字符串构造出来。

最后一个细节就是最后一行不需要均匀分配空格，句尾留空就可以，所以要单独处理一下。

时间上我们需要扫描单词一遍，然后在找到行尾的时候在扫描一遍当前行的单词，不过总体每个单词不会被访问超过两遍，所以总体时间复杂度是O(n)。而空间复杂度则是结果的大小（跟单词数量和长度有关，不能准确定义，如果知道最后行数r，则是O(r*L)）。代码如下： 

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