# Remove Invalid Parentheses
### 题目描述

>Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.
Note: The input string may contain letters other than the parentheses ( and ).

##### Example
>"()())()" -> ["()()()", "(())()"]
"(a)())()" -> ["(a)()()", "(a())()"]
")(" -> [""]

[原题链接](https://leetcode.com/problems/remove-invalid-parentheses/description/)


### 解题思路

- Limit max removal rmL and rmR for backtracking boundary 因为括号必须配对. Otherwise it will exhaust all possible valid substrings, not shortest ones.
- Scan from left to right, avoiding invalid strs (on the fly) by checking num of open parens.
- If it's '(', either use it, or remove it.
- If it's '(', either use it, or remove it.
- Otherwise just append it.
Lastly set StringBuilder to the last decision point.

In each step, make sure:
- i does not exceed s.length().
- Max removal rmL rmR and num of open parens are non negative.
- De-duplicate by adding to a HashSet.

###  Java代码实现

``` java
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        int rmL = 0, rmR = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                rmL++;
            } else if (s.charAt(i) == ')') {
                if (rmL != 0) {
                    rmL--;
                } else {
                    rmR++;
                }
            }
        }
        Set<String> res = new HashSet<>();
        dfs(s, 0, res, new StringBuilder(), rmL, rmR, 0);
        return new ArrayList<String>(res);
    }
    
    public void dfs(String s, int i, Set<String> res, StringBuilder sb, int rmL, int rmR, int open) {
        if (rmL < 0 || rmR < 0 || open < 0) {
            return;
        }
        if (i == s.length()) {
            if (rmL == 0 && rmR == 0 && open == 0) {
                res.add(sb.toString());
            }        
            return;
        }

        char c = s.charAt(i); 
        int len = sb.length();

        if (c == '(') {
            dfs(s, i + 1, res, sb, rmL - 1, rmR, open);		    // not use '('
            dfs(s, i + 1, res, sb.append(c), rmL, rmR, open + 1);       // use '('

        } else if (c == ')') {
            dfs(s, i + 1, res, sb, rmL, rmR - 1, open);	            // not use  ')'
            dfs(s, i + 1, res, sb.append(c), rmL, rmR, open - 1);  	    // use ')'

        } else {
            dfs(s, i + 1, res, sb.append(c), rmL, rmR, open);	
        }

        sb.setLength(len);        
    }
}
```