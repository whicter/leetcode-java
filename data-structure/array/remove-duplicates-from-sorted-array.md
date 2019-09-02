# 26. Remove Duplicates from Sorted Array

### 题目描述

>Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.
<br>
<br>Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

#### Example 1
> Given nums = <span style="background-color:#ffe6e6"><font color=#cc0000 >[1, 1, 2]</font></span>,
<br>Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
<br>It doesn't matter what you leave beyond the returned length.

#### Example 2
>Given nums = <span style="background-color:#ffe6e6"><font color=#cc0000 >[0, 0, 1, 1, 1, 2, 2, 3, 3, 4]</font></span>,
<br>Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.
<br>It doesn't matter what values are set beyond the returned length.

[原题链接](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

### 解题思路
明确 f[i] 的原子操作：
假设a[0 -> i]已经处理完，无重复元素的数组长度为 len
1. 如果 a[i] == a[len - 1]:
    Do nothing
2. 如果a[i] != a[len - 1]:
    则a[len] = a[i];
    len ++

base case: 
因为有len - 1， 所以len >= 1。所以 i 从 1 开始计数    

#### Java代码实现

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length < 2) { 
            return nums.length;
        }
        
        int len = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[len - 1]) {
                nums[len] = nums[i];
                len ++;
            }
        }
        return len;
    }
}
```