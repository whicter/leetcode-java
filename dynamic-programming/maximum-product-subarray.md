# 152. Maximum Product Subarray
### 题目描述
> Given an integer array nums, find the contiguous subarray within an array (containing at least one number) which has the largest product.

#### Example 1:

    Input: [2,3,-2,4]
    Output: 6
    Explanation: [2,3] has the largest product 6.

#### Example 2:

    Input: [-2,0,-1]
    Output: 0
    Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
    
[原题链接](https://leetcode.com/problems/maximum-subarray/)

### 解题思路
同样是非常经典的全局最优和局部最优的维护。
这里需要注意的是有负负得正会得到更大的数，因此需要同时**维护两个局部最优**：preMin 和 preMax
因为有可能preMin是负数，当前也是负数会得到新的max

原子操作
- f(i): 以a[i] 为结尾的subarry的最大积
f(i) = max{a[i] \* f(i - 1), a[i] \* g(i - 1), a[i]}

- g(i): 以a[i] 为结尾的subarry的最小积
g(i) = min{a[i] \* f(i - 1), a[i] \* g(i - 1), a[i]}


于此同时维护global

#### Java 代码实现
```java
class Solution {
    public int maxProduct(int[] nums) {
        
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int preMin = nums[0];
        int preMax = nums[0];
        int max = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            int curNum = nums[i];
            
            // need to include curNum into comparison since there would be 0 
            int curMin = Math.min(preMin * curNum, Math.min(curNum, preMax * curNum));
            int curMax = Math.max(preMin * curNum, Math.max(curNum, preMax * curNum));
            
            preMin = curMin;
            preMax = curMax;
            
            max = Math.max(max, curMax);
        }
        
        return max;
    }
}
```


