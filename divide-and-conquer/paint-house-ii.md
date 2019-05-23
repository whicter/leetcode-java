# 265. Paint House II

### 题目描述

>There are a row of n houses, each house can be painted with one of the k colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

>The cost of painting each house with a certain color is represented by a n x k cost matrix. For example, costs[0][0] is the cost of painting house 0 with color 0; costs[1][2] is the cost of painting house 1 with color 2, and so on... Find the minimum cost to paint all houses.

>**Note**:
All costs are positive integers.

#### Example
    Input: [[1,5,3],[2,9,4]]
    Output: 5
    Explanation: Paint house 0 into color 0, paint house 1 into color 2. Minimum cost: 1 + 4 = 5; 
                 Or paint house 0 into color 2, paint house 1 into color 0. Minimum cost: 3 + 2 = 5. 

**Follow up**:
Could you solve it in O(nk) runtime?

[原题链接](https://leetcode.com/problems/paint-house-ii/)

### 解题思路

线性问题。对于原子操作f[i]:
- 房子i的最小cost为j，而0 -> i - 1的最小cost对应的 i - 1的cost坐标**不为j**
<br> 则 0 -> i - 1的最小cost为[i][j] + minCost(0 -> i - 1)

- 房子i的最小cost为j，而0 -> i - 1的最小cost对应的 i - 1的cost坐标**也是j**
<br> 则 0 -> i - 1的最小cost为[i][j] + secMinCost(0 -> i - 1)

根据以上的推导，就需要维护三个变量：
1. 0 -> i 的最小cost
2. 0 -> i 的第二小cost
3. 0 -> i 的最小cost对应的颜色坐标 (j)

在遍历房子i的每一个cost的时候，可以不断更新curMin, curSecMin 以及 minIdx

### Java代码实现：

```java
class Solution {
    public int minCostII(int[][] costs) {
        if (costs == null || costs.length == 0) {
            return 0;
        }
        
        int prevMinCost = 0; 
        int prevSecCost = 0; 
        int prevMinIdx = -1;
        
        for (int i = 0; i < costs.length; i ++) {
            // 找出最小和次小的，以及该轮最小cost的下标
            int currMin = Integer.MAX_VALUE; 
            int currSecMin = Integer.MAX_VALUE; 
            int currIdx = -1;
            
            for (int j = 0; j < costs[0].length; j++) {
                int costAt_i_j = costs[i][j] + (prevMinIdx == j ? prevSecCost : prevMinCost);
                
                if(costAt_i_j < currMin){
                    currSecMin = currMin;
                    currMin = costAt_i_j;
                    currIdx = j;
                } else if (costAt_i_j < currSecMin){
                    currSecMin = costAt_i_j;
                }
            }
            prevMinCost = currMin;
            prevSecCost = currSecMin;
            prevMinIdx = currIdx;
        }
        return prevMinCost;
    }
}
```

