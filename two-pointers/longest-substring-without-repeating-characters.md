# 3. Longest Substring Without Repeating Characters

### 题目描述

>Given a string, find the length of the longest substring without repeating characters.

#### Example 1:

    Input: "abcabcbb"
    Output: 3 
    Explanation: The answer is "abc", with the length of 3. 

#### Example 2:

    Input: "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.

#### Example 3:

    Input: "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3. 
                 Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
                 
[原题链接](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

### 解题思路
Sliding window， 同时用HashMap来保存字符的位置
需要注意的是如果出现新的字符，我们需要比较charMap.get(cur) + 1 和start，因为很有可能现在的sliding window的start已经在该字符上一次出现的很后面了

#### Java代码实现

``` java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int start = 0;
        int maxLen = 0;
        Map<Character, Integer> charMap = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++) {
            char cur = s.charAt(i);
            if (charMap.containsKey(cur)) {
                // Math.max is need since if there is another duplicated letter appears, the start will jump back which we don't want it.
                start = Math.max(charMap.get(cur) + 1, start); 
            }
            maxLen = Math.max(maxLen, i - start + 1);
            charMap.put(cur, i);
        }
        return maxLen; 
    }
}
```