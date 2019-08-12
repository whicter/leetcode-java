# 560. Subarray Sum Equals K

### 题目描述

>Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

#### Example
>**Input: **nums = [1,1,1], k = 2
**Output: **2

**Note:**
1. The length of the array is in range [1, 20,000].
2. The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].


[原题链接](https://leetcode.com/problems/subarray-sum-equals-k/)


### 解题思路
方法1. 二层循环
方法2. 存在递归关系：$$sum(i, j) = sum(0, j) - sum(0, i)$$。因此我们建立一个HashMap, 结构为：($$sum_i$$, no.ofOccurencesOf$$Sum_i$$)。需要注意的是初始状况，需要`preSum.put(0, 1);

####  Java代码实现

``` java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int sum = 0, result = 0;
        Map<Integer, Integer> preSum = new HashMap<>();
        preSum.put(0, 1);
        
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (preSum.containsKey(sum - k)) {
                result += preSum.get(sum - k);
            }
            preSum.put(sum, preSum.getOrDefault(sum, 0) + 1);
        }
        
        return result;
    }
}
```