# 100. Same Tree

### 题目描述

>Given two binary trees, write a function to check if they are equal or not.
Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

[原题链接](https://leetcode.com/problems/same-tree/description/)

### 解题思路
一个queue解决一层一层比较
###  Java代码实现

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        
        Queue<TreeNode> nodeQueue = new LinkedList<>();
        nodeQueue.offer(p);
        nodeQueue.offer(q);
        
        while (!nodeQueue.isEmpty()) {
            TreeNode node1 = nodeQueue.poll();
            TreeNode node2 = nodeQueue.poll();
            
            if (node1 == null && node2 != null || node1 != null && node2 == null) {
                return false;
            } else if (node1 == null || node2 == null) {
                continue;
            } else {
                if (node1.val == node2.val) {
                    nodeQueue.offer(node1.left);
                    nodeQueue.offer(node2.left);
                    nodeQueue.offer(node1.right);
                    nodeQueue.offer(node2.right);
                } else {
                    return false;
                }
            }
                
        }
        
        return true;
    }
}
```