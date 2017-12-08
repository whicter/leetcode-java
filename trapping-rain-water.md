# 42. Trapping Rain Water

### 题目描述

>Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

>For example, 
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.

![](/assets/Trapping rain water.png)
The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. 


[原题链接](https://leetcode.com/problems/trapping-rain-water/)

### 解题思路
移动pointer条件：
lMax和rMax中较小的那个

可以想象成这么一个过程：初始状态有两块板（height array的首尾）然后中间没有任何凹槽。每次移动指针就好比是插入新的板。如果新板的高度比max大，那显然不可能有新的水可以加入，同时需要更新max。反之则说明有了新的凹槽可以存水，且新加入的存储水的量是有max - height[i]来决定

代码中加入了判断来找到第一对可能可以存水的高度：因为递增的左边或者递减的右边是无法存水的。当然这一部分判断也是optional的不影响最终的结果

###  Java代码实现

``` java
public class Solution {
    public int trap(int[] height) {

        int left = 0, right = height.length - 1;
        int lMax = 0;
        int rMax = 0;

        int res = 0;

        // find the left and right edge which can hold water  
        while (left < right && height[left] <= height[left + 1]) {
            left++;  
        }
        while (left < right && height[right] <= height[right - 1]) {
            right--;  
        }

        while (left < right) {
            lMax = Math.max(lMax, height[left]); // max within [0..left]
            rMax = Math.max(rMax, height[right]); // max within [right..n-1]

            if (lMax < rMax) {
                res += lMax - height[left++];
            }
            else {
                res += rMax - height[right--];
            }
        }
        return res;
    }
}
```