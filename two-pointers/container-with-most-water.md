#11. Container With Most Water

### 题目描述

>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.
![](/assets/Container With Most Water.png)
### Example
    Input: [1,8,6,2,5,4,8,3,7]
    Output: 49

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

### Java代码实现

``` java
class Solution {
    public int maxArea(int[] height) {
        int left = 0, right = height.length - 1;
        int maxArea = 0;
        
        while (left < right) {
            maxArea = Math.max(maxArea, (right - left) * Math.min(height[left], height[right]));
            if (height[left] < height[right]) {
                left ++;
            } else {
                right --;
            }
        }
        return maxArea;
    }
}
```