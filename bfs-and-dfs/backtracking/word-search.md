# 51. N-Queens

### 题目描述

>Given a 2D board and a word, find if the word exists in the grid.
<br>The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

### Example:

    board =
    [
        ['A','B','C','E'],
        ['S','F','C','S'],
        ['A','D','E','E']
    ]

    Given word = "ABCCED", return true.
    Given word = "SEE", return true.
    Given word = "ABCB", return false.



[原题链接](https://leetcode.com/problems/word-search/)

### 解题思路
DFS深度优先。先找到起始点，然后开始向四个方向分别DFS。每次标记一下访问的点，然后在DFS结束后，回溯——取消标记

### Java代码实现：

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;

        boolean result = false;
        for (int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
               if (findPathDfs(board, i, j, word, 0)){
                   result = true;
               }
            }
        }

        return result;

    }
    
    public boolean findPathDfs(char[][] board, int row, int col, String word, int wordIdx) {
        int m = board.length;
        int n = board[0].length;
        
        if (row < 0 || row >= m || col < 0 || col >= n) {
            return false;
        }
        char curChar = board[row][col];
        if (curChar == word.charAt(wordIdx)) {
            board[row][col] = '#'; //visited
            
            if (wordIdx == word.length() - 1) {
                return true;
            } else if (
                findPathDfs(board, row + 1, col, word, wordIdx + 1) 
                 || findPathDfs(board, row, col + 1, word, wordIdx + 1)
                 || findPathDfs(board, row - 1, col, word, wordIdx + 1)
                 || findPathDfs(board, row, col - 1, word, wordIdx + 1)
                ) {
                return true;
            
            }
            board[row][col] = curChar; // backtrack
        }
        return false;
    }
}
```

