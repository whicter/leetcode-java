# 80. Remove Duplicates from Sorted Array II
### 题目描述

>Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.
<br>
<br>Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

#### Example 1
> Given nums = <span style="background-color:#ffe6e6"><font color=#cc0000 >[1, 1, 1, 2, 2, 3],</font></span>,
<br>Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.
<br>It doesn't matter what you leave beyond the returned length.

#### Example 2
>Given nums = <span style="background-color:#ffe6e6"><font color=#cc0000 >[0, 0, 1, 1, 1, 1, 2, 3, 3]</font></span>,
<br>Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.
<br>It doesn't matter what values are set beyond the returned length.

[原题链接](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

### 解题思路
与第26题一样，这次进行len - 2操作即可  

#### Java代码实现

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length < 3) { 
            return nums.length;
        }
        
        int len = 2;
        for (int i = 2; i < nums.length; i++) {
            if (nums[i] != nums[len - 2]) {
                nums[len] = nums[i];
                len ++;
            }
        }
        return len;
    }
}
```