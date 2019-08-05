# 1026. Maximum Difference Between Node and Ancestor

### 题目描述
Given the root of a binary tree, find the maximum value V for which there exists different nodes A and B where V = |A.val - B.val| and A is an ancestor of B.

(A node A is an ancestor of B if either: any child of A is equal to B, or any child of A is an ancestor of B.)

 

### Example:
    Input: [8,3,10,1,6,null,14,null,null,4,7,13]
    Output: 7
    Explanation: 
    We have various ancestor-node differences, some of which are given below :
    |8 - 3| = 5
    |3 - 7| = 4
    |8 - 1| = 7
    |10 - 13| = 3
    Among all possible differences, the maximum value of 7 is obtained by |8 - 1| = 7.

**Note:**

1. The number of nodes in the tree is between 2 and 5000.
2. Each node will have value between 0 and 100000.


[原题链接](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/)

### 解题思路
此题技巧在于，每个节点和祖先节点的最大的差，是出现在当前节点和min Ancestor和max Ancestor之中。因此题目也转化为树的DFS遍历过程中维护最大和最小的ancestor

### Java代码实现-DFS：

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
    private int maxDiff = Integer.MIN_VALUE;
    
    public int maxAncestorDiff(TreeNode root) {
        int minAncestor = Integer.MIN_VALUE;
        int maxAncestor = Integer.MAX_VALUE;
        
        dfs(root, root.val, root.val);
        
        return maxDiff;
        
    }
    
    private void dfs(TreeNode node, int minAncestor, int maxAncestor) {
        if (node != null) {
            int curNodeVal = node.val;
            int diff1 = Math.abs(curNodeVal - minAncestor);
            int diff2 = Math.abs(curNodeVal - maxAncestor);
            
            maxDiff = Math.max(maxDiff, Math.max(diff1, diff2));
            
            dfs(node.left, Math.min(minAncestor, curNodeVal), Math.max(maxAncestor, curNodeVal));
            
            dfs(node.right, Math.min(minAncestor, curNodeVal), Math.max(maxAncestor, curNodeVal));
        }
    }
}
```



