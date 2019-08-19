# 238. Product of Array Except Self

### 题目描述

> Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

#### Example:

    Input:  [1,2,3,4]
    Output: [24,12,8,6]
    
**Note:** Please solve it without division and in O(n).

**Follow up:**
Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)

[原题链接](https://leetcode.com/problems/product-of-array-except-self/)

### 解题思路

两次遍历，一次从前往后，在i存下product from 0 -> i - 1; 一次从后往前，在原有的基础上叠加len - 1 -> i + 1

#### Java代码实现

```java
class Solution {
	public int[] productExceptSelf(int[] nums) {
		int pro[] = new int[nums.length];
		pro[0] = 1;
		for (int i = 1; i < nums.length; i++) {

			pro[i] = pro[i - 1] * nums[i - 1];
		}

		int right = 1;

		for (int j = nums.length - 1; j >= 0; j--) {
			pro[j] = pro[j] * right;
			right = right * nums[j];
		}
		return pro;
	}
}
```