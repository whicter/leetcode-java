# 505. The Maze II
### 题目描述

>There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.
<br>Given the ball's start position, the destination and the maze, find the shortest distance for the ball to stop at the destination. The distance is defined by the number of empty spaces traveled by the ball from the start position (excluded) to the destination (included). If the ball cannot stop at the destination, return -1.
<br>The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.

### Example

    Input 1: a maze represented by a 2D array

    0 0 1 0 0
    0 0 0 0 0
    0 0 0 1 0
    1 1 0 1 1
    0 0 0 0 0

    Input 2: start coordinate (rowStart, colStart) = (0, 4)
    Input 3: destination coordinate (rowDest, colDest) = (4, 4)

    Output: 12

    Explanation: One shortest way is : left -> down -> left -> down -> right -> down -> right.
                The total distance is 1 + 1 + 3 + 1 + 2 + 2 + 2 = 12.
   ![](/assets/The Maze II_1.png)             

### Example 2:

    Input 1: a maze represented by a 2D array

    0 0 1 0 0
    0 0 0 0 0
    0 0 0 1 0
    1 1 0 1 1
    0 0 0 0 0

    Input 2: start coordinate (rowStart, colStart) = (0, 4)
    Input 3: destination coordinate (rowDest, colDest) = (3, 2)

    Output: -1

    Explanation: There is no way for the ball to stop at the destination.

![](/assets/The Maze II_2.png)


**Note:**

- There is only one ball and one destination in the maze.
- Both the ball and the destination exist on an empty space, and they will not be at the same position initially.
- The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
- The maze contains at least 2 empty spaces, and both the width and height of the maze won't exceed 100.
[原题链接](https://leetcode.com/problems/the-maze-ii/)

### 解题思路

非常好的BFS题。一般求最短路径，BFS相对更容易理解和实现，遍历所有的合法路径，找到最优解。

对于队列里每一个坐标，从当前位置开始，每次尝试4个可能的方向，然后遇到1就停止， 把前面的位置加入到queue里面，并得到新坐标并更新到达该坐标的最小步数

### Java代码实现

``` java
class Solution {
    public int shortestDistance(int[][] maze, int[] start, int[] dest) {
        int[][] movingDirect = {{-1,0}, {1,0},{0,-1}, {0,1}};
        
        Queue<int[]> queue = new LinkedList<>();
        queue.add(start);
        
        // initialize results set
        int[][] minDist = new int[maze.length][maze[0].length];
        for (int i = 0; i < minDist.length; ++i) {
            Arrays.fill(minDist[i], Integer.MAX_VALUE);
        }
        
        minDist[start[0]][start[1]] = 0;
        
        while (!queue.isEmpty()) {
            int[] curNode = queue.poll();
            
            for (int i = 0; i < movingDirect.length; i++) {
                // get new coordinates
                int newX = curNode[0] + movingDirect[i][0];
                int newY = curNode[1] + movingDirect[i][1];
                
                int curStep = minDist[curNode[0]][curNode[1]];
                while (newX >= 0 && newX < maze.length 
                       && newY >= 0 && newY < maze[0].length 
                       && maze[newX][newY] == 0) {                    
                    newX += movingDirect[i][0];
                    newY += movingDirect[i][1];
                    curStep++;
                }
                
                // boundry or block reached, need to step back to get the reachable pos
                newX -= movingDirect[i][0];  
                newY -= movingDirect[i][1];
                
                // update minDist to (newX, newY) if needed;
                if (curStep < minDist[newX][newY]) {
                    minDist[newX][newY] = curStep;
                    queue.add(new int[]{newX, newY});
                }
                             
            }
        }
        
        return minDist[dest[0]][dest[1]] == Integer.MAX_VALUE ? -1 : minDist[dest[0]][dest[1]];
        
    }
}
```