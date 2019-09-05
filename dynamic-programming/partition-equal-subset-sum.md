# 416. Partition Equal Subset Sum
### 题目描述
> Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

- Each of the array element will not exceed 100.
- The array size will not exceed 200.
 

#### Example 1:

    Input: [1, 5, 11, 5]
    Output: true
    Explanation: The array can be partitioned as [1, 5, 5] and [11].
 

#### Example 2:

    Input: [1, 2, 3, 5]
    Output: false
    Explanation: The array cannot be partitioned into equal sum subsets.
    
[原题链接](https://leetcode.com/problems/partition-equal-subset-sum/)

### 解题思路
首先判断可否等分，如果total sum不是偶数那一定没办法等分。如果是偶数，那1/2的total sum就是目标和，因此题目也转化为是否存在目标和的子集

可以这样思考，找到在nums里是否存在目标和为sum的子集，可以分解为，对于每一个nums[i], 在去掉nums[i]的集合里是否存在目标和为sum - num[i]的子集

定义原子操作$$f(sum, i)$$为在$$从1st -> ith$$元素序列中是否存在和为$$sum$$的子集

$$f(sum, i) = f(sum - num[i], nums[i - 1])$$, for all $$0 -> i$$


递推公式为： $$dp[i][j] = dp[i - 1][j]$$ || $$dp[i - 1][j - nums[i - 1]]$$
需要注意的是，$$i$$在$$dp[][]$$中的含义是第$$i$$项

#### Java 代码实现
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
        }
        if (sum % 2 != 0) {
            return false;
        }
        
        sum = sum / 2;
        
        int n = nums.length;

		// T[i][j] stores true if subset with sum j can be attained
		// with using items up to first i items
		boolean[][] T = new boolean[n + 1][sum + 1];

		// if sum is zero, empty subset counts
		for (int i = 0; i <= n; i++) {
			T[i][0] = true;
		}

		// do for ith item
		for (int i = 1; i <= n; i++) {
			// consider all sum from 1 to sum
            int curNum = nums[i - 1];
			for (int j = 1; j <= sum; j++) {
				// don't include ith element if j - curNum is negative
				if (curNum > j) {
					T[i][j] = T[i - 1][j];
				}
				else {
					// find subset with sum j by excluding or including
					// the ith item
					T[i][j] = T[i - 1][j] || T[i - 1][j - curNum];
				}
			}
		}
        
        /* Another way to think about the loop
        for (int j = 1; j <= sum; j++) {
            for (int i = 1; i <= n; i++) {
                if (nums[i - 1] > j) {
                    T[i][j] = T[i - 1][j];
                } else {
                    T[i][j] = T[i - 1][j] || T[i - 1][j - nums[i - 1]];
                }
            }
        }
        */
        
        return T[n][sum];
    }
}
```


