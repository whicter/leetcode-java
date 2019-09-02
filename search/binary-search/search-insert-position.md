# 35. Search Insert Position
### 题目描述

> Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
><br><br>You may assume no duplicates in the array.

### Example 1:
    Input: [1,3,5,6], 5
    Output: 2

### Example 2:
    Input: [1,3,5,6], 2
    Output: 1

### Example 3:
    Input: [1,3,5,6], 7
    Output: 4

### Example 4:
    Input: [1,3,5,6], 0
    Output: 0

[原题链接](https://leetcode.com/problems/search-insert-position/)



### 解题思路
需要注意的是返回的index和对应的边界情况
1. 如果没有找到target且start 和 end都还在数组中间，那自然就返回start - 1即可，因为循环的退出条件是start > end
2. 如果没有找到且start已经出了边界，返回start。此时需要在数组之后添加该数字
3. 如果没有找到且end已经出了边界，返回0。此时需要在数组之前添加该数字

因此有如下代码：
```java
    if (nums.length == start) {
        return start;
    } else if (end == -1) {
        return 0;
    } else {
        return start;
    }
```

这个循环还能简化，请见下方AC代码
此题虽然容易，但是若不小心也很容易出错

#### Java代码实现

``` java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                start ++;
            } else {
                end --;
            }
        }
        if (end == -1) {
            return 0;
        } else {
            return start;
        }
    }
}
```