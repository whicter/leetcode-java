# 138. Single Number III
### 题目描述

>Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

#### Example
Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

[原题链接](https://leetcode.com/problems/single-number-iii/description/)

### 解题思路
这题有两个数字都只出现了一次，那么我们如果能想办法把原数组分为两个小数组，不相同的两个数字分别在两个小数组中，这样分别调用Single Number 单独的数字的解法就可以得到答案。

1. 通过遍历整个数组并求整个数组所有数字之间的 XOR，根据 XOR 的特性可以得到最终的结果为 AXORB = A XOR B；

2. 因为A 和 B 是不相同的，所以他们的二进制数字有且至少有一位是不相同的。我们将这一位设置为 1，并将所有的其他位设置为 0，为了方便起见，我们用 a & ~(a - 1) 来取出最右端为‘1’的位。 我们假设我们得到的这个数字为 bitFlag；

3. 其余的数字在这个bit上，或为0， 或为1。那我们只需要在循环一次数组，将与上 bitFlag 为 0 的数字进行 XOR 运算，与上 bitFlag 不为 0 的数组进行独立的 XOR 运算。那么最后我们得到的这两个数字就是 A 和 B。

#### Java代码实现

```java
class Solution {
    public int[] singleNumber(int[] nums) {
        int xorResult = 0;
        
        for (int i = 0; i < nums.length; i++) {
            xorResult ^= nums[i];
        }
        int bit = xorResult & ~(xorResult - 1);
        
        int num1 = 0, num2 = 0;
        for (int num : nums) {
            if ((num & bit) == 0) {
                num1 ^= num;
            } else {
                num2 ^= num;
            }
        }
        
        return new int[]{num1, num2};
    }
}
```





