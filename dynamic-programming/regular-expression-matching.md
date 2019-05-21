# 10. Regular Expression Matching
### 题目描述

>Implement regular expression matching with support for <span style="background-color:#ffe6e6"><font color=#cc0000 >'.'</font></span>
and <span style="background-color:#ffe6e6"><font color=#cc0000 >'*'</font></span>.


    '.' Matches any single character.
    '*' Matches zero or more of the preceding element.
    The matching should cover the entire input string (not partial).
    The function prototype should be:
    bool isMatch(const char *s, const char *p)
    Some examples:
    isMatch("aa","a") → false
    isMatch("aa","aa") → true
    isMatch("aaa","aa") → false
    isMatch("aa", "a*") → true
    isMatch("aa", ".*") → true
    isMatch("ab", ".*") → true
    isMatch("aab", "c*a*b") → true

[原题链接](https://leetcode.com/problems/regular-expression-matching/description/)

### 解题思路
D[i][j]: 表示string s中取i长度的字串，string p中取j长度字串，进行匹配。
D[0][0] 表示什么都不取，所以二位dp的长度应该为[s.length + 1][p.length + 1]

- p[j]不是'*'。情况比较简单，只要判断如果当前s的i和p的j上的字符一样（如果有p在j上的字符是'.',也是相同），并且res[i][j]==true，则res[i + 1][j + 1]也为true，res[i + 1][j + 1]=false; 

- p[j]是 '*'，但是p[j - 1] != '.'。那么只要以下条件有一个满足即可对res[i + 1][j + 1]赋值为true： 
- res[i + 1][j]为真（'*'只取前面字符一次）; 
- res[i + 1][j - 1]为真（'*'前面字符一次都不取，也就是忽略这两个字符）; 
- res[i][j + 1] && s[i]==s[i - 1] && s[i - 1] == p[j - 1]。(这种情况是相当于i从0到s.length()扫过来，如果p[j]对应的字符是‘\*’那就意味着接下来的串就可以依次匹配下来，如果下面的字符一直重复，并且就是‘\*’前面的那个字符）。

    因为是＊号，所以意味着如果重复就可以一直匹配下去，也就是前面相等（res[i][j + 1]）， 然后字符重复（s[i]==s[i - 1] ），并且重复的字符就是*号前面的字符（s[i - 1] == p[j - 1]）， 这几个条件满足时就可以满足匹配

- p[j + 1]是 '\*'，并且p[j] == '.'。因为 '\.\*' 可以匹配任意字符串，所以在前面的res[i + 1][j - 1]或者res[i + 1][j]中只要有i + 1是true，那么剩下的res[i + 1][j + 1], res[i + 2][j + 1], ..., res[s.length()][j + 1]就都是true了。



状态转移方程如下：
1. If p.charAt(j) == s.charAt(i) : dp[i][j] = dp[i - 1][j - 1];
2. If p.charAt(j) == '.' : dp[i][j] = dp[i - 1][j - 1];
3. If p.charAt(j) == '*': 
    - if p.charAt(j - 1) != s.charAt(i): 
    <br>dp[i][j] = dp[i][j - 2]  //in this case, a* only counts as empty
    - if p.charAt(j - 1) == s.charAt(i) or p.charAt(i - 1) == '.':
        - dp[i][j] = dp[i - 1][j] //in this case, a* counts as multiple a
        - or dp[i][j] = dp[i][j - 1] // in this case, a* counts as single a
        - or dp[i][j] = dp[i][j - 2] // in this case, a* counts as empty
        
### Java代码实现

``` java
class Solution {
    public boolean isMatch(String s, String p) {

        if (s == null || p == null) {
            return false;
        }
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        dp[0][0] = true;
        for (int i = 0; i < p.length(); i++) {
            if (p.charAt(i) == '*' && dp[0][i - 1]) {
                dp[0][i + 1] = true;
            }
        }
        for (int i = 0 ; i < s.length(); i++) {
            for (int j = 0; j < p.length(); j++) {
                if (p.charAt(j) == '.' || p.charAt(j) == s.charAt(i)) {
                    dp[i + 1][j + 1] = dp[i][j];
                }

                if (p.charAt(j) == '*') {
                    if (p.charAt(j - 1) != s.charAt(i) && p.charAt(j - 1) != '.') {
                        dp[i + 1][j + 1] = dp[i + 1][j - 1];
                    } else {
                        dp[i + 1][j + 1] = (dp[i + 1][j] || dp[i][j + 1] || dp[i + 1][j - 1]);
                    }
                }
            }
        }
        return dp[s.length()][p.length()];
    }
}
```