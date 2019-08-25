# 128. Longest Consecutive Sequence
### 题目描述

> Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(n) complexity.

#### Example:

    Input: [100, 4, 200, 1, 3, 2]
    Output: 4
    Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.


[原题链接](https://leetcode.com/problems/two-sum/description/)

### 解题思路
因为需要O(n)就不能排序。我们考虑维护一个hashmap，key为数字，value为包含key的最长连续子串的长度

遍历数字的时候如果数字不在map里，我们会试图在map里找到 num + 1 和 num - 1 对应的长度，然后相加再加1就是包括当前数字的最长的子串长度。然后更新 num + 1 的 end 和 num - 1 对应的 end 的连续子串长度

如果map里已经有num则直接跳过，因为这个数字一定已经有对应的且是最新的包含该数字的连续子串长度

####  Java代码实现

``` java
class Solution {
    public int longestConsecutive(int[] nums) {
        // Key: num; Value: longest consecutive sequence with num being part of it
        Map<Integer, Integer> map = new HashMap<>();
        int maxLen = 0;
        
        for (int num : nums) {
            if (!map.containsKey(num)) {
                int left = map.getOrDefault(num - 1, 0);
                int right = map.getOrDefault(num + 1, 0);
                
                int len = left + right + 1;
                maxLen = Math.max(maxLen, len);
                
                map.put(num, len);
                
                // update lenth for boundary value
                map.put(num - left, len);
                map.put(num + right, len);
                
            }
        }
        return maxLen;
    }
}
```