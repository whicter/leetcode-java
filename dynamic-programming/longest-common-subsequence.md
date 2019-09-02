# 1143. Longest Common Subsequence
### 题目描述

>Given two strings text1 and text2, return the length of their longest common subsequence.
<br><br>A subsequence of a string is a new string generated from the original string with some characters(can be none) deleted without changing the relative order of the remaining characters. (eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings is a subsequence that is common to both strings.
<br><br>If there is no common subsequence, return 0.

#### Example 1:

    Input: text1 = "abcde", text2 = "ace" 
    Output: 3  
    Explanation: The longest common subsequence is "ace" and its length is 3.

#### Example 2:

    Input: text1 = "abc", text2 = "abc"
    Output: 3
    Explanation: The longest common subsequence is "abc" and its length is 3.



[原题链接](https://leetcode.com/problems/longest-common-subsequence/)

### 解题思路
我们定义dp[i][j] 为str1匹配到i，str匹配到j的时候的最长公共序列

如果$$c(i) == c(j)$$, $$dp[i][j] = dp[i - 1][j - 1] + 1$$
反之，则 $$dp[i][j] = max\{dp[i - 1][j], dp[i][j - 1]\}$$

base case为 $$i = j = 0$$，这时候我们会发现一个问题，$$i - 1$$和$$j - 1$$没有意义。因此我们更改一下我们的定义：

$$dp[i + 1][j + 1]$$ 为str1匹配到i，str匹配到j的时候的最长公共序列


### Java代码实现：

```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int dp[][] = new int[text1.length() + 1][text2.length() + 1];
        
        for (int i = 0; i < text1.length(); i++) {
            char c1 = text1.charAt(i);
            for (int j = 0; j < text2.length(); j++) {
                char c2 = text2.charAt(j);
                if (c1 == c2) {
                    dp[i + 1][j + 1] = dp[i][j] + 1; // java int array is automatically initiallized with 0s
                } else {
                    dp[i + 1][j + 1] = Math.max(dp[i + 1][j], dp[i][j + 1]);
        
                }
            }
        }
        return dp[text1.length()][text2.length()];
    }
}
```

