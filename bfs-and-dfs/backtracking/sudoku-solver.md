# 37. Sudoku Solver

### 题目描述

>Write a program to solve a Sudoku puzzle by filling the empty cells.
>
>A sudoku solution must satisfy all of the following rules:
>
>Each of the digits 1-9 must occur exactly once in each row.
>Each of the digits 1-9 must occur exactly once in each column.
>Each of the the digits 1-9 must occur exactly once in each of the 9 3x3 sub-boxes of the grid.
>Empty cells are indicated by the character '.'.

**Note**:

The given board contain only digits 1-9 and the character '.'.
You may assume that the given Sudoku puzzle will have a single unique solution.
The given board size is always 9x9.

[原题链接](https://leetcode.com/problems/sudoku-solver/)

### 解题思路

递归回溯来尝试每一个数字，每次来验证**行**，**列**，以及**九宫格**里是否有重复数字

##### 九宫格的坐标
- 假设给定row, col, 九宫格的起始坐标为：row / 3 * 3, col / 3 * 3
- 当对九宫格进行遍历时，九宫格的内部坐标为：i / 3, i % 3

![](/assets/Sudoku Solver_box_index.png)

### Java代码实现：

```java
class Solution {
    public void solveSudoku(char[][] board) {
        if (board == null || board.length == 0) return;
        solve(board);
    }
    
    private boolean solve(char[][] board) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                
                if (board[i][j] == '.') {
                    for (char ch = '1'; ch <= '9'; ch++) {
                        if (isValid(board, i, j, ch)) {
                            board[i][j] = ch;
                            if (solve(board)) {
                                return true;
                            } else {
                                board[i][j] = '.';
                            }
                        }
                    }
                    return false;
                }
                
            }
        }
        return true;
    }
    
    private boolean isValid(char[][] board, int row, int col, char ch) {
        for (int i = 0; i < 9; i++) {
            if (board[i][col] == ch 
                || board[row][i] == ch 
                || board[row / 3 * 3 + i / 3][col / 3 * 3 + i % 3] == ch)  {
                return false;
            }
        }
        return true;
    }
}

```


