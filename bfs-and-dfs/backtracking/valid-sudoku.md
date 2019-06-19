# 36. Valid Sudoku

### 题目描述

> Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:
>    - Each row must contain the digits 1-9 without repetition.
>    - Each column must contain the digits 1-9 without repetition.
>    - Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

**Note**:

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.
- The given board contain only digits 1-9 and the character '.'.
- The given board size is always 9x9.

[原题链接](https://leetcode.com/problems/sudoku-solver/)

### 解题思路

- 行无重复
- 列无重复
- 九宫格内部无重复

因此对于这三者分别有三个Array of Set，array inde x为行（列，九宫格）数

##### 九宫格编号

* 假设给定row, col, 九宫格的编号为： box_index = (row / 3) * 3 + col / 3

![](/assets/Sudoku Solver_box_index.png)

### Java代码实现：

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        // init data
        Set<Integer> [] rows = new HashSet[9];
        Set<Integer> [] columns = new HashSet[9];
        Set<Integer> [] boxes = new HashSet[9];
        for (int i = 0; i < 9; i++) {
          rows[i] = new HashSet<Integer>();
          columns[i] = new HashSet<Integer>();
          boxes[i] = new HashSet<Integer>();
        }
        
        for (int row = 0; row < board.length; row++) {
            for (int col = 0; col < board[0].length; col++) {
                char numChar = board[row][col];
                if (numChar != '.') {
                    int num = Character.getNumericValue(numChar);
                    int box_index = (row / 3 ) * 3 + col / 3 ;
                    
                    if (rows[row].contains(num) || columns[col].contains(num) || boxes[box_index].contains(num)) {
                        return false;
                    }
                    rows[row].add(num);
                    columns[col].add(num);
                    boxes[box_index].add(num);
                }
                
            }
        }
        return true;
    }
}
```


