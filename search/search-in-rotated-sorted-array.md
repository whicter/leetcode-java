# Search in Rotated Sorted Array
### 题目描述

> Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
<br> (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
<br> You are given a target value to search. If found in the array return its index, otherwise return -1.
<br> You may assume no duplicate exists in the array.

[原题链接](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

### 解题思路
Revised binary search. 鉴于每次要去掉一半，单纯对比mid和target无法找到新的起始点，所以需要比较num[start] / num[end] 与mid的关系来确定中位数在哪半边。如果在左半边且start < target < mid，则可以确定新的end = mid - 1；如果在右半边且mid < target < end，则新的start = mid + 1;

纠结于到底是start < end 还是 <= 很容易的判断办法就是小样本corner case。如果是 < ，那当array只有一个元素且是target的时候，根本进不去loop

###  Java代码实现

``` java
class Solution {
    public int search(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > nums[end]) {
                // left side sorted
                if (target <= nums[mid] && target >= nums[start]) {
                    end = mid - 1;
                } else {
                    start = mid + 1;
                }
            } else {
                // right side sorted
                if (target >= nums[mid] && target <= nums[end]) {
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            }
            
        }
        return - 1;
    }          
}
```