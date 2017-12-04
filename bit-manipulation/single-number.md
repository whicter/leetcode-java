# 136. Single Number
### 题目描述

>Given an array of integers, every element appears twice except for one. Find that single one.

[原题链接](https://leetcode.com/problems/single-number/description/)

### 解题思路
XOR operation:
x^x = 0, x^0 = x and XOR operator is commutative
#### Java代码实现

```java
class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;
        
        for (int i = 0; i < nums.length; i++) {
            // x^x = 0, x^0 = x and XOR operator is commutative
            result ^= nums[i];
        }
        return result;
    }
}
```
