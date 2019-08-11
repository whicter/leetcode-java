# 1. Two Sum
### 题目描述

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.You may assume that each input would have exactly one solution, and you may not use the same element twice.

#### Example
> Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1]. 

[原题链接](https://leetcode.com/problems/two-sum/description/)

### 解题思路
因为需要返回原数组的index，所以不能排序
HashMap来记录当前数值和位置，如果当前数值的counterpart存在于map中可直接返回结果
###  Java代码实现

``` java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                result[0] = map.get(target - nums[i]);
                result[1] = i;
                break;
            } 
            map.put(nums[i], i);
        }
        return result;
    }
}
```