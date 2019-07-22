# 684. Redundant Connection
### 题目描述

>In this problem, a tree is an undirected graph that is connected and has no cycles.
<br>The given input is a graph that started as a tree with N nodes (with distinct values 1, 2, ..., N), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.
<br>The resulting graph is given as a 2D-array of `edges`. Each element of edges is a pair `[u, v]` with `u < v`, that represents an undirected edge connecting nodes `u` and `v`.
<br>Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge `[u, v]` should be in the same format, with `u < v`.

### Example 1:

    Input: [[1,2], [1,3], [2,3]]
    Output: [2,3]
    Explanation: The given undirected graph will be like this:
      1
     / \
    2 - 3
    Example 2:

### Example 2: 
    Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
    Output: [1,4]
    Explanation: The given undirected graph will be like this:
    5 - 1 - 2
        |   |
        4 - 3

**Note:**

- The size of the input 2D-array will be between 3 and 1000.
- Every integer represented in the 2D-array will be between 1 and N, where N is the size of the input array.

[原题链接](https://leetcode.com/problems/redundant-connection/)



### 解题思路
并查集基本模板


### Java代码实现

``` java
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int[] parents = new int[edges.length * 2];
        for (int i = 0; i < parents.length; i++) {
            parents[i] = i;
        }
        
        for (int[] edge: edges){
            int node1 = edge[0], node2 = edge[1];
            if (find(parents, node1, node2)) {
                return edge;
            } else {
                union(parents, node1, node2);
            }
        }
        
        return new int[2]; // no redundant connection found
    }
    
    private int getRoot(int[] parents, int node) {
        if (node != parents[node]) {
          parents[node] = getRoot(parents, parents[node]);  
        }
        return parents[node];
    }

    private boolean find(int[] parents, int node1, int node2) {
        return getRoot(parents, node1) == getRoot(parents, node2);
    }

    private void union(int[] parents, int node1, int node2) {
        parents[getRoot(parents, node2)] = getRoot(parents, node1); 
    }
}
```