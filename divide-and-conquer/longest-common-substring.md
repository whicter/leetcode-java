# 79. Longest Common Substring

### 题目描述

> Given two strings, find the longest common substring.

### Example 1:
	Input:  "ABCD" and "CBCE"
	Output:  2
	
	Explanation:
	Longest common substring is "BC"


### Example 2:
	Input: "ABCD" and "EACB"
	Output:  1
	
	Explanation: 
	Longest common substring is 'A' or 'C' or 'B'




[原题链接](https://www.lintcode.com/problem/longest-common-substring/description)

### 解题思路
经典动态规划题，但是不要一上来就套dp公式，思考过程更重要
一般这样明显的线性问题，还是要找原子操作。在这里涉及到两个String，那我们需要定义原子操作f(i, j)， i和j为两个字符串的pointer:

1. s1[i] == s2[j]
    显然f(i, j) = f(i - 1, j - 1)
2. s1[i] != s2[j]
    那LCS一定不包含s1[i]或s2[j]，即：不会以s1[i] / s2[j]作为起始也不会作为结尾。因此f(i, j) = 0;    

在遍历过程中，维护一个全局的max来找到最大值
有些follow up会需要打印字符串，那每次max在更新的时候，更新一下endOfS1 或者 endOfS2

```java
public class Solution {
    /**
     * @param A: A string
     * @param B: A string
     * @return: the length of the longest common substring.
     */
    public int longestCommonSubstring(String A, String B) {
        int m = A.length();
        int n = B.length();

        int max = 0;
        int endOfi;

        int[][] dp = new int[m][n];

        for (int i = 0; i < m; i++){
            for (int j = 0; j < n; j++){
                if (a.charAt(i) == b.charAt(j)){
                    if (i == 0 || j == 0){
                        dp[i][j] = 1;
                    } else {
                        dp[i][j] = dp[i - 1][j - 1] + 1;
                    }

                    if (max < dp[i][j]) {
                        max = dp[i][j];
                        endOfi = i;
                    }
                }

            }
        }

        return max;
    }
}
```



