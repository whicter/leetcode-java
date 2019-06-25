# 104. Maximum Depth of Binary Tree

### 题目描述

> Given a binary tree, find its maximum depth.

> The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.  

[原题链接](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

###  Java代码实现1 - 递归

``` java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public int maxDepth(TreeNode root) {
        return root == null ? 0 : Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

###   Java代码实现2 - BFS

``` java
public class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int count = 0;
        while (!queue.isEmpty()) {
            int remainingLevelSize = queue.size();
            while (remainingLevelSize-- > 0) {
                TreeNode curNode = queue.poll();
                nodeEnqueue(curNode.left, queue);
                nodeEnqueue(curNode.right, queue);
            }
            count ++;
        } 
        return count;
    }
    
    private void nodeEnqueue(TreeNode curNode, Queue<TreeNode> queue) {
        if (curNode != null) {
            queue.offer(curNode);
        }
    }
}
```