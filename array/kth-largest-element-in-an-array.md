# 215. Kth Largest Element in an Array

### 题目描述

> Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.


<br> Given <span style="background-color:#ffe6e6"><font color=#cc0000 >[3,2,1,5,6,4]</font></span> and k = 2, return 5.

#### Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.

[原题链接](https://leetcode.com/problems/rotate-array/description/)

### 解题思路

Application of quick selection



#### Java代码实现

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        
        if (nums == null || nums.length == 0) {
            return Integer.MAX_VALUE;
        }
        return quickSelect(nums, 0, nums.length - 1, nums.length - k);
    }
        
    public int quickSelect(int[]nums, int left, int right, int k) {
        int pivot = nums[right];
        int partition = left;
        for (int i = left; i < right; i++) {
            if (nums[i] <= pivot) {
                swap(nums, partition++, i);
            }
        }
        swap(nums, partition, right);
    
        if (k == partition) {
            return nums[partition];
        } else if (k < partition) {
            return quickSelect(nums, left, partition - 1, k);
        } else {
            return quickSelect(nums, partition + 1, right, k);
        }
        
    }
    
    private void swap(int[] A, int i, int j) {
    	int tmp = A[i];
    	A[i] = A[j];
    	A[j] = tmp;				
    }
}
```





