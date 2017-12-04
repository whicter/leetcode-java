# 268. Missing Number
### 题目描述

>Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

#### Example 1
>Input: [3,0,1]
<br>Output: 2

#### Example 2
>Input: [9,6,4,2,3,5,7,0,1]
<br>Output: 8

[原题链接](https://leetcode.com/problems/missing-number/description/)

### 解题思路
还是利用XOR的思路。数组的长度的值是必须出现在整个sequence里，所以我们可以直接预设res = nums.length，然后每次对数字和index做异或。

#### Java代码实现

```java
class Solution {
    public int missingNumber(int[] nums) {
        int res = nums.length;
        for (int i = 0; i < nums.length; i++) {
            res = res ^ i ^ nums[i];
        }
        return res;
    }
}
```





