#75. Sort Colors

### 题目描述

> Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

#### Example:

    Input: [2,0,2,1,1,0]
    Output: [0,0,1,1,2,2]

**Follow up:**

- A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
- Could you come up with a one-pass algorithm using only constant space?

[原题链接](https://leetcode.com/problems/sort-colors/)

### 解题思路
两块挡板三个区域：
- 所有的`0`都在0 -> i - 1
- 所有的`2`都在k + 1 -> len - 1
- 中间的区域为1和尚未遍历的元素（i -> j - 1即为`1`）

中间的j作为iterator

- 每次遇到0，和i的数字swap。根据以上的定义，swap完，i的位置就是0， j就是1。因此两者同时前进
- 每次遇到2，和k的数字swap。根据以上的定义，swap完，k的位置就是0， 但是j的位置不知道换回来了什么。因此k后退，j原地不动

#### Java代码实现
``` java
class Solution {
    public void sortColors(int[] nums) {
        int i = 0, j = 0, k = nums.length - 1;
        
        while(j <= k) {
            if (nums[j] == 0) {
                swap(nums, i, j);
                i++;
                j++;
            } else if (nums[j] == 2) {
                swap(nums, j, k);
                k--;
                
            } else {
                j++;
            }
        }
        
    }
    
    private void swap(int[] nums, int pos1, int pos2) {
        int temp = nums[pos1];
        nums[pos1] = nums[pos2];
        nums[pos2] = temp;
    }
}
```