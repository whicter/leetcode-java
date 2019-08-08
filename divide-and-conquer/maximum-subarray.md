# 53. Maximum Subarray
### 题目描述
> Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

### Example:

    Input: [-2,1,-3,4,-1,2,1,-5,4],
    Output: 6
    Explanation: [4,-1,2,1] has the largest sum = 6.


[原题链接](https://leetcode.com/problems/maximum-subarray/)

### 解题思路
题目很简单，但是非常经典的全局最优和局部最优的维护

原子操作f(i): 以a[i] 为结尾的subarry的最大和
- f(i) = a[i] + f(i - 1), if a[i] + f(i - 1) > a[i]
- f(i) = a[i], if a[i] + f(i - 1) < a[i]

于此同时维护global

```java
public class Solution {
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int res = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            nums[i] = Math.max(nums[i], nums[i - 1] + nums[i]);
            res = Math.max(res, nums[i]);
        }
        return res;
    }
}
```


