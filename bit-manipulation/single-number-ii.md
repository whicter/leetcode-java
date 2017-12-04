# 137. Single Number III
### 题目描述

>Given an array of integers, every element appears three times except for one, which appears exactly once. Find that single one.

[原题链接](https://leetcode.com/problems/single-number-ii/description/)

### 解题思路
由于x^x^x = x，无法直接利用I的方法来解。但可以应用类似的思路，即利用位运算来消除重复3次的数。以一个数组[14 14 14 9]为例，将每个数字以二进制表达：

1110
1110
1110
1001
_____
4331    对每一位进行求和
1001    对每一位的和做%3运算，来消去所有重复3次的数

[14, 14, 14, 9]
i = 0, j = 4, bit = 1
1
result = 1
i = 1, j = 4, bit = 3
0
result = 1
i = 2, j = 4, bit = 3
0
result = 1
i = 3, j = 4, bit = 4
1
result = 9
#### Java代码实现

```java
class Solution {
    public int singleNumber(int[] nums) {
        int i, j, bit, result = 0;

        for (i = 0; i < 32; i++) {
            for (j = bit = 0; j < nums.length; j++) {
                // if ith digit from right of num[j] is 1, then bit++
                if (((nums[j] >> i) & 1) == 1) {
                    bit++;
                }
            }
            // System.out.println("i = " + i + ", j = " + j + ", bit = " + bit);
          
            bit = bit % 3;
           
            result |= bit << i;
            //System.out.println("result = " + result);
        }

        return result;
    }
}
```





