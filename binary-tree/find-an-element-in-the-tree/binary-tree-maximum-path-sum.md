# 124. Binary Tree Maximum Path Sum

### 题目描述

> Given a non-empty binary tree, find the maximum path sum.
>
>For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

#### Example 1
Input: [1, 2, 3]

       1
      / \
     2   3

Output: 6

#### Example 2
Input: [-10, 9, 20, null, null, 15, 7]

      -10
       / \
      9  20
        /  \
       15   7

Output: 42

[原题链接](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

### 解题思路
#### 情景1：最大路径和包含root
则路径可能为
- 包含左节点的最大路径 + root
- 包含右节点的最大路径 + root
- 1 + 2

#### 情景2：最大路径存在于某个子树中，如example 2

因此需要计算的变量有：
- 包含左节点的最大路径
- 包含右节点的最大路径
- 当前节点视角里的最大路径
    

#### Java代码实现

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int maxSum = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        
        findMaxSum(root);
        return maxSum;
    }
    private int findMaxSum(TreeNode curNode) {
        if (curNode == null) {
            return 0;
        } else {
            // 包含左节点的最大路径和
            int maxSumLeft = findMaxSum(curNode.left);
            //包含右节点的最大路径和
            int maxSumRight = findMaxSum(curNode.right);
            
            int curNodeVal = curNode.val;
            int curMax = curNodeVal;
            
            // 包含当前节点的最大路径和
            if (maxSumLeft > 0) {
                curMax = curMax + maxSumLeft;
            } 
            
            if (maxSumRight > 0) {
                curMax = curMax + maxSumRight;
            }
            
            maxSum = Math.max(curMax, maxSum);
            
            // 向上一层返回 以当前节点为起始点的最大路径和
            return Math.max(curNode.val, Math.max(curNode.val + maxSumLeft, curNode.val + maxSumRight));
        }
    }
}
```