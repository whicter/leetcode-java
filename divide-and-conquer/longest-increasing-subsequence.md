# 300. Longest Increasing Subsequence

### 题目描述

>Given an unsorted array of integers, find the length of longest increasing subsequence.

#### Example:

    Input: [10,9,2,5,3,7,101,18]
    Output: 4 
    Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
    
**Note**
- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(n2) complexity.
Follow up: Could you improve it to O(n log n) time complexity?

[原题链接](https://leetcode.com/problems/longest-increasing-subsequence/)

### 解题思路
#### 解法一：标准DP
线性问题。对于原子操作f[i]:

f[i] = max{f[0], f[1], ...., f[i - 1]} + 1, if nums[k] < nums[i] for k < i

else f[i] == 1


#### Java代码实现：

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        int len = 0;
        for (int num : nums) {
            int i = Arrays.binarySearch(dp, 0, len, num);
            if (i < 0) {
                i = -(i + 1);
            }
            dp[i] = num;
            if (i == len) {
                len++;
            }
        }
        return len;
    }
}
```
#### 解法二：DP + Binary Search
具体解释见：https://www.acwing.com/solution/leetcode/content/287/

> 在解法1中，对于每个i，都需要遍历dp[1]到dp[i-1]，但其实是不必要的，因为dp[i] = max(dp[j] + 1), 1 ≤ j < i 且 nums[j] < nums[i]，那么对于 j而言，希望dp[j]越大越好，nums[j]越小越好。那么在数组中，若nums[p] ≥ nums[q]但 dp[p]≤dp[q]，那么对于求dp[i]来说，nums[p]是没有用的。

> <br>例如在数组[1, 2, 5, 3, 7, 8]中，nums[2] = 5,dp[2] = 3（序列[1, 2, 5], nums[3] = 3, dp[3] = 3（序列[1, 2, 3]），那么对于数组中下一个数字7来说，下标为2的5就是没有用的，因为存在下标3，使得nums[3] < nums[2]
且dp[3] ≥ dp[2]，那么我们就不用考虑下标为2的数字5了。

> <br>建立数组dp表示表示最长子序列长度为i时的最小的结尾num值。我们只需要找到找到最大的满足help[j] < m 的 j，那么就意味着把 m 接在 help[j] 这个数字后面就可以了，这个子序列的长度是j + 1.

> <br>同时我们需要判断 m 是否比原来的help[j + 1]小，如果m更小的话就需要更新help[j + 1] = m，这一定是一个单调递增的数组（因为要求子序列必须是单调递增的，那么序列长度为i + 1的子序列最后一个数字一定比序列长度为i的子序列最后一个数字要大），那么我们就可以通过二分查找来找到满足条件的 j 

#### Java 代码实现
```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        int result = -1;
        for (int i = 0; i < nums.length; i++) {
            if (result == -1 || dp[result] < nums[i]) {
                result++;
                dp[result] = nums[i];
            } else {
                int index = this._binarySearch(dp, 0, result, nums[i]);
                dp[index] = nums[i];
                result = Math.max(result, index);
            }
        }
        
        return result + 1;
    }
    
    private int _binarySearch(int[] nums, int head, int tail, int target) {
        while (head <= tail) {
            int mid = (head + tail) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                head = mid + 1;
            } else {
                tail = mid - 1;
            }
        }
        
        return head;
    }
}
```
 



