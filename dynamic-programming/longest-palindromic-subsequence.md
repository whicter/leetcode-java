# 516. Longest Palindromic Subsequence

### 题目描述

> Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

#### Example 1:
    Input:
    
    "bbbab"
    Output:
    4
    One possible longest palindromic subsequence is "bbbb".

#### Example 2:
    Input:
    
    "cbbd"
    Output:
    2
    One possible longest palindromic subsequence is "bb".

[原题链接](https://leetcode.com/problems/longest-palindromic-subsequence/)

### 解题思路

判断一个序列是否是palindrome我们需要两个端点，因此定义 $$f(i, j)$$
 为 $$S(i) -> S(j)$$ 的最长palindrome string

- $$S(i) == S(j)$$ 则 $$f(i, j) = f(i + 1, j - 1) + 2$$
- $$S(i) != S(j)$$ 则 $$f(i, j) = Max\{f(i + 1, j), f(i, j - 1)\}$$

由于 $$i$$ 取决于 $$i + 1$$，$$j$$ 取决于 $$j - 1$$ 且 $$j > i$$, 所以在循环的时候，$$i$$ 从 $$size - 1$$ 开始，$$j$$ 从 $$i + 1$$开始
#### Java代码实现：

```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        int size = s.length();
        int[][] dp = new int[size][size];
        
        // i starts from len - 1, from big to small, because to calcule the dp[i][j], we need the value dp[i+1][j-1], so we need to reverse the order. 
        for (int i = size - 1; i >= 0; i--) {
            dp[i][i] = 1;
            for (int j = i + 1; j < size; j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[0][size - 1];
    }
}
```

