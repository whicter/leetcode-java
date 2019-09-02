# 74. Search a 2D Matrix

> Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

> - Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

#### Example 1:

    Input:
    matrix = [
      [1,   3,  5,  7],
      [10, 11, 16, 20],
      [23, 30, 34, 50]
    ]
    target = 3
    Output: true

#### Example 2:

    Input:
    matrix = [
      [1,   3,  5,  7],
      [10, 11, 16, 20],
      [23, 30, 34, 50]
    ]
    target = 13
    Output: false
  
[原题链接](https://leetcode.com/problems/search-a-2d-matrix/)



### 解题思路
如果把这个matrix完全展开成一维就是一个完全升序的数组，所以二分搜索。每次得到的mid值可以通过`mid / col, mid % col`来获取对应行列

#### Java代码实现

``` java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            return false;
        }
        int row = matrix.length;
        int col = matrix[0].length;
        
        int begin = 0, end = row * col - 1;
        
        while (begin <= end) {
            int mid = begin + (end - begin) / 2;
            int midVal = matrix[mid / col][mid % col];
            if (target == midVal) {
                return true;
            } else if (target < midVal) {
                end = mid - 1;
            } else {
                begin = mid + 1;
            }
        }
        return false;
    }
}
```  