# 200. Number of Islands
### 题目描述

> Given a 2d grid map of <span style="background-color:#ffe6e6"><font color=#cc0000 >'1'</font></span>
s (land) and <span style="background-color:#ffe6e6"><font color=#cc0000 >'0'</font></span>
s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

#### Example 1
> 11110
> 11010
> 11000
> 00000

Answer: 1

#### Example 2
> 11000
> 11000
> 00100
> 00011

Answer: 3


[原题链接](https://leetcode.com/problems/number-of-islands/description/)


### 解题思路

DFS。以“陆地”点为基点，向四个方向分别进行dfs知道遇到“海洋”的点。

小技巧在于将dfs中访问过的陆地点标记为海洋，或者建立一个二维boolean来标记visited，这样就避免重复搜索

####  Java代码实现

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
        
        boolean[][] visited = new boolean[row][col];

        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (grid[i][j] == '1' && !visited[i][j]) {
                    num ++;
                    dfs(grid, i, j, visited);
                }
            }
        }
        return num;
    }

    public void dfs(char[][] grid, int i, int j, boolean[][] visited) {
        if (i < 0 || i >= grid.length 
            || j < 0 || j >= grid[0].length
            || visited[i][j]
           ) {
            return;
        }   

        if (grid[i][j] == '1') {
            visited[i][j] = true;
            dfs(grid, i - 1, j, visited);
            dfs(grid, i + 1, j, visited);
            dfs(grid, i, j - 1, visited);
            dfs(grid, i, j + 1, visited);
        }
    }
}
```