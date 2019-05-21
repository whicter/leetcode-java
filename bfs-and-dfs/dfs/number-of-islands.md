# 200. Number of Islands
### 题目描述

> Given a 2d grid map of <span style="background-color:#ffe6e6"><font color=#cc0000 >'1'</font></span>
s (land) and <span style="background-color:#ffe6e6"><font color=#cc0000 >'0'</font></span>
s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

#### Example 1
> 11110
<br> 11010
<br> 11000
<br> 00000

Answer: 1

#### Example 2
> 11000
<br> 11000
<br> 00100
<br> 00011

Answer: 3


[原题链接](https://leetcode.com/problems/number-of-islands/description/)


### 解题思路

DFS。以“陆地”点为基点，向四个方向分别进行dfs知道遇到“海洋”的点。小技巧在于将dfs中访问过的陆地点标记为海洋，这样就避免重复搜索

###  Java代码实现

``` java
class Solution {
    public int numIslands(char[][] grid) {
        int num = 0;
        
        int row = grid.length;
        if (row == 0) {
            return num;
        }
        int col = grid[0].length;
        if (col == 0) {
            return num;
        }
        
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (grid[i][j] == '1') {
                    num ++;
                    dfs(grid, i, j);
                }
            }
        }
        return num;
    }
    
    public void dfs(char[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length) {
            return;
        }   
        
        if (grid[i][j] == '1') {
            grid[i][j] = '0';
            dfs(grid, i - 1, j);
            dfs(grid, i + 1, j);
            dfs(grid, i, j - 1);
            dfs(grid, i, j + 1);
        }
    }
}
```