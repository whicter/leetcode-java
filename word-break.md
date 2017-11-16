# Word Break
### 题目描述

>Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

##### Example
>s = <span style="background-color:#ffe6e6"><font color=#cc0000 >"leetcode"</font></span>
<br>dict = <span style="background-color:#ffe6e6"><font color=#cc0000 >["leet", "code"]</font></span>.
<br>Return true because <span style="background-color:#ffe6e6"><font color=#cc0000 >"leetcode"</font></span> can be segmented as <span style="background-color:#ffe6e6"><font color=#cc0000 >"leet code"</font></span>.

[原题链接](https://leetcode.com/problems/word-break/description/)

### 解题思路
不需要记录具体结果同时大问题可以被分割成小问题，符合DP特征
###  Java代码实现

``` java

/*
    递归有重复计算：当在循环到时候，会多次计算从i到j的子序列是否存在于字典中
    故而考虑使用DP： dp(i) = dp(j) && s[j, i) in dict
*/
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if (wordDict == null || wordDict.isEmpty()) {
            return false;
        }
        
        Set wordSet = new HashSet(wordDict);
        
        // 表示字符串的前i项可以被分割
        // 因为substring取不到第i项，所以需要多一格
        boolean result[] = new boolean[s.length() + 1];
        result[0] = true;
        
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (result[j] && wordSet.contains(s.substring(j, i))) {
                    result[i] = true;
                    break;
                }
            }
        }
        
        return result[s.length()];
    }
}
```
