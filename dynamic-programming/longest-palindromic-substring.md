# 5. Longest Palindromic Substring

### 题目描述

> Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

#### Example 1:

    Input: "babad"
    Output: "bab"
    Note: "aba" is also a valid answer.

#### Example 2:

    Input: "cbbd"
    Output: "bb"




[原题链接](https://leetcode.com/problems/longest-palindromic-substring/)

### 解题思路
定义原子操作$$f(i)$$: 当我们指针走到i的时候，需要找出所有以i结尾的回文子串以及长度，即：
$$Max\{s(k, ...., i)\}$$ where $$k < i$$ and $$s(k, ...., i)$$ is Palindrome

判断$$s(k, ...., i)$$是否为回文串又可以分解为：$$s(k) == s(i)$$ && $$s(k + 1, ...., i - 1)$$ is palindrome

因此为了记录历史信息，构造二维$$dp[i][j] == true$$ if $$s(i,....,j)$$ is palindrome


#### Java 代码实现

```java
class Solution {

    public String longestPalindrome(String s) {
        if (s.length() == 0) {
            return "";
        }
	
	//dp[i][j] == true if s(i,....,j) is palindrome
        boolean[][] dp = new boolean[s.length()][s.length()];
        int start = 0, end = 0;

        for (int i = 0; i < s.length(); ++i) {
            for (int j = i; j >= 0; --j) {
                boolean startEqEnd = s.charAt(j) == s.charAt(i);

                if (i == j) {
                    //If the same char: 'a' is palindrome
                    dp[i][j] = true;
                    
                } else if (i - j == 1) {
                    //If length 2: 'ab' is palindrome when 'a' == 'b'
                    dp[i][j] = startEqEnd;
                    
                } else if (startEqEnd && dp[i - 1][j + 1]) {
                    //Otherwise: string is palindrome if s(i) == s(j) and substring s(j + 1, i - 1) is palindrome
                    dp[i][j] = true;
                }

                if (dp[i][j] && i - j > end - start ) {
                    end = i;
                    start = j;
                }
            }
        }

        return s.substring(start, end + 1);
    }
}
```



