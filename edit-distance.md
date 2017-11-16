# 72. Edit Distance
### 题目描述

> Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)  
<br> You have the following 3 operations permitted on a word:
<br> a) Insert a character
<br> b) Delete a character
<br> c) Replace a character

[原题链接](https://leetcode.com/problems/edit-distance/discuss/)

### 解题思路
维护二位数组dp[i][j]用来表示从初始状态到达word1[0, i] 和word[0, j]所需要的操作数

Case 1: word1[i] == word2[j], 
f(i, j) = f(i - 1, j - 1)

Case 2: word1[i] != word2[j], 有三种操作，即添加，删除，替换
f(i, j) = 1 + min { f(i, j - 1), f(i - 1, j), f(i - 1, j - 1) }
f(i, j - 1)：insert operation
f(i - 1, j) ：delete operation
f(i - 1, j - 1) ：replace operation

###  Java代码实现

``` java
class Solution {
    public int minDistance(String word1, String word2) {
        if (word1.equals(word2)) {
            return 0;
        }
        if (word1.length() == 0 || word2.length() == 0) {
            return Math.abs(word1.length() - word2.length());
        }
        int len1 = word1.length();
        int len2 = word2.length();
        
        int[][] dp = new int[len1 + 1][len2 + 1];
        
        for (int i = 0; i <= len1; i++) {
            dp[i][0] = i;
        }
        
        for (int j = 0; j <= len2; j++) {
            dp[0][j] = j;
        }
        
        for (int i = 0; i <= len1; i++) {
            for (int j = 0; j <= len2; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
                }
            }
        }
        return dp[len1][len2];
    }
}
```