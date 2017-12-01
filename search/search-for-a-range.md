# 34. Search for a Range
### 题目描述

> Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.
<br>Your algorithm's runtime complexity must be in the order of O(log n).
<br>If the target is not found in the array, return [-1, -1].

#### Example,
>Given <span style="background-color:#ffe6e6"><font color=#cc0000>
[5, 7, 7, 8, 8, 10]</font></span> and target value 8,
<br>return <span style="background-color:#ffe6e6"><font color=#cc0000 >
[3, 4]</font></span>.

[原题链接](https://leetcode.com/problems/search-for-a-range/description/)

### 解题思路
Binary Search的变体，第一次找到最左边，第二次找最右边。关键部分代码如下：
找最左边的时候：
``` java
            if (nums[mid] == target) {
                idx = mid;
                end = mid - 1;
            }
```

找最右边的时候：
``` java
            if (nums[mid] == target) {
                idx = mid;
                start = mid - 1;
            }
```


###  Java代码实现

``` java
public class Solution {
    public int[] searchRange(int[] A, int target) {
        int left = findFirst(A, target);
        int right = findLast(A, target);
        int[] res = {left, right};
        if (left == -1) {
            res[0] = right;
        } 
        
        if (right == -1) {
            res[1] = left;
        }
        return res;
    }
    
    private int findFirst(int[] nums, int target){
        int idx = -1;
        int start = 0;
        int end = nums.length - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                idx = mid;
                end = mid - 1;
            } else if (nums[mid] > target) {
                end = mid - 1;
            } else { 
                start = mid + 1;
            }
        
        }
        return idx;
    }

    private int findLast(int[] nums, int target){
        int idx = -1;
        int start = 0;
        int end = nums.length - 1;
        while (start <= end){
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                idx = mid;
                start = mid + 1;
            } else if (nums[mid] < target) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return idx;
    }
}
```