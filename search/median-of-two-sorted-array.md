# 4. Median of Two Sorted Arrays
### 题目描述

> There are two sorted arrays nums1 and nums2 of size m and n respectively.
Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

##### Example 1
> nums1 = [1, 3]
<br> nums2 = [2]
<br> The median is 2.0

##### Example 2:
>nums1 = [1, 2]
<br> nums2 = [3, 4]
<br> The median is (2 + 3)/2 = 2.5

[原题链接](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

### 解题思路
This problem can be converted to the problem of finding kth element, k is (A's length + B' Length)/2.
If any of the two arrays is empty, then the kth element is the non-empty array's kth element. If k == 0, the kth element is the first element of A or B.
For normal cases(all other cases), we need to move the pointer at the pace of half of the array size to get log(n) time.

![](/assets/median_of_two_sorted_arrays.png)

###  Java代码实现

``` java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int total = nums1.length + nums2.length;
        if (total % 2 == 0) {
            return (findKth(total / 2 + 1, nums1, nums2, 0, 0) + findKth(total / 2, nums1, nums2, 0, 0)) / 2.0;
        } else {
            return findKth(total / 2 + 1, nums1, nums2, 0, 0);
        }
        
    }

     private int findKth(int k, int[] nums1, int[]nums2, int start1, int start2) {
        int len1 = nums1.length, len2 = nums2.length;
        
        if (start1 >= len1) {
            return nums2[start2 + k - 1];
        }
        
        if (start2 >= len2) {
            return nums1[start1 + k - 1];
        }
        
        if (k == 1) {
            return Math.min(nums1[start1], nums2[start2]);
        }
        
        int m1 = start1 + k / 2 - 1;
        int m2 = start2 + k / 2 - 1;
        
        int middle1 = m1 >= len1 ? Integer.MAX_VALUE : nums1[m1];
        int middle2 = m2 >= len2 ? Integer.MAX_VALUE : nums2[m2];
        
        if (middle1 < middle2) {
            return findKth(k - k / 2, nums1, nums2, start1 + k / 2, start2);
        } else {
            return findKth(k - k / 2, nums1, nums2, start1, start2 + k / 2);
        }
    }
}
```