# 658. Find K Closest Elements
### 题目描述

> Given a sorted array, two integers k and x, find the k closest elements to x in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred.

### Example 1:
    Input: [1,2,3,4,5], k=4, x=3
    Output: [1,2,3,4]

### Example 2:
Input: [1,3,5,6], 2
Output: 1

### Example 3:
    Input: [1,2,3,4,5], k=4, x=-1
    Output: [1,2,3,4]


**Note:**

The value k is positive and will always be smaller than the length of the sorted array.

Length of the given array is positive and will not exceed 10<sup>4</sup>

Absolute value of elements in the array and x will not exceed 10<sup>4</sup>


[原题链接](https://leetcode.com/problems/find-k-closest-elements/)

### 解题思路
- 解法一： 
类似于暴力解，时间复杂度很高，思路就是：二分找到x在数组里的插入位置，再在数组里的那个位置向左和向右看，每次加进去一个，直到加满k个

- 解法二：
直接从数组里通过二分法找到应为的subarray的start位置，通过判断mid位置和mid + k位置上与x的差值的大小比较来确定二分的update rule，因此时间复杂度更好。需要注意mid + k的边界问题

### Java代码实现
**解法一**
``` java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> result = new ArrayList<>();
        if (arr.length == 0) return result;
        int index = findInsert(arr, x);
        int count = 0;
        int left = index;
        int right = index;
        if (arr[index] == x) {
            result.add(arr[index]);
            count ++;
            left --;
            right ++;
        } else if (index == 0) {
            for (int i = 0; i < k; i++) {
                if (i >= arr.length) {
                    break;
                }
                result.add(arr[i]);
            }
            return result;
        } else {
            left = left - 1;
        }
        
        while (count < k) {
            if (left < 0) {
                result.add(arr[right]);
                right ++;
                count ++;
            } else if (right > arr.length - 1 || arr[right] - x >= x - arr[left]) {
                result.add(0, arr[left]);
                left --;
                count ++;
            } else {
                result.add(arr[right]);
                right ++;
                count ++;
            }
        }
        return result;
    }
    public int findInsert(int[] nums, int target) {
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

**解法二**
```java
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> res = new ArrayList<>();
        int start = 0, end = arr.length - k;
        while (start <= end){
            int mid = start + (end-start) / 2;
            if (mid + k >= arr.length) {
                break;
            } else if(Math.abs(arr[mid] - x) > Math.abs(arr[mid + k] - x)){ 
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        for (int i = start; i < start + k; i++){
            res.add(arr[i]);
        }
        return res;
    }
}
```