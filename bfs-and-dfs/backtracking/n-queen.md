# 51. N-Queens

### 题目描述

>The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.
>
>Given an integer n, return all distinct solutions to the n-queens puzzle.
>Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

#### Example:
    Input: 4
    Output: [
        [".Q..",  // Solution 1
        "...Q",
        "Q...",
        "..Q."],

        ["..Q.",  // Solution 2
        "Q...",
        "...Q",
        ".Q.."]
    ]
    Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above.



[原题链接](https://leetcode.com/problems/n-queens/)

### 解题思路

从题目的输出要求来看，要逐行打印，那我们需要一个二维数组来存Q的位置。简化后，我们可以有一个一位数组，下标为列，数值为Q的行位置

#### 如何唯一确定Q的位置？
由于我们是逐列对棋盘进行扫描，所以我们仅需要知道，对于该列的每一行i，是否在同一行，主对角线和付对角线上存在Q。我们可以用三个集合来存储信息

**对角线特征**
- 主对角线row + col 值相同
- 副对角线row - col 值相同

每次放置完Q后，对下一列进行递归，同时回溯剪枝

### Java代码实现：

```java
class Solution {
    
    List<List<String>> finalResults = new LinkedList<List<String>>();
    
    Set<Integer> rowSet = new HashSet<Integer>();
    Set<Integer> diag1Set = new HashSet<Integer>(); // 副对角线
    Set<Integer> diag2Set = new HashSet<Integer>(); // 主对角线
    
    public List<List<String>> solveNQueens(int n) {
        generateResult(new LinkedList<Integer>(), n, 0);
        return finalResults;
    }
    
    // for curPos, the index means column and value means row
    private void generateResult(LinkedList<Integer> curPos, int n, int curColumn) {
        // column starts at 0; when cur column == n means we make to the final stage with all queens properly placed
        if (curColumn == n) {
            List<String> curResult = new ArrayList<>();
            for (Integer pos: curPos) {
                StringBuilder sb = new StringBuilder();
                for (int row = 0; row < n; i++) {
                    if (row != pos) {
                        sb.append('.');
                    } else {
                        sb.append('Q');
                    }
                }
                curResult.add(sb.toString());
            }
            finalResults.add(curResult);
        } else {
            for (int row = 0; row < n; row++) {
                int diag1 = row + curColumn;
                int diag2 = row - curColumn;

                if (rowSet.contains(row) || diag1Set.contains(diag1) || diag2Set.contains(diag2)) {
                    continue;
                }

                // update temp result
                curPos.add(row);
                rowSet.add(row);
                diag1Set.add(diag1);
                diag2Set.add(diag2);

                generateResult(curPos, n, curColumn + 1);

                // backtracking
                diag2Set.remove(diag2);
                diag1Set.remove(diag1);
                rowSet.remove(row);
                curPos.removeLast();
            }
        }
    }
}
```


