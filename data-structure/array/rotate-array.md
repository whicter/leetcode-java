# 189. Rotate Array
### 题目描述

> Rotate an array of n elements to the right by k steps.
<br> For example, with _n = 7 _and _k = 3_, the array 
<span style="background-color:#ffe6e6"><font color=#cc0000 >[1,2,3,4,5,6,7]</font></span> is rotated to <span style="background-color:#ffe6e6"><font color=#cc0000 >[5,6,7,1,2,3,4]</font></span>.

**Note:**
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

[原题链接](https://leetcode.com/problems/rotate-array/description/)

### 解题思路

常用技巧：
- 翻转全部
- 逐个部分再做翻转

这样可以保证没有额外空间，此类方法同样适用于String rotation




#### Java代码实现

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int len = nums.length;
        k = k % len;
        
        reverseArray(nums, 0, len - 1);
        reverseArray(nums, 0, k - 1);
        reverseArray(nums, k, len - 1);
        
    }
    public void reverseArray(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;

            start ++;
            end --;
        }
    }
}
```