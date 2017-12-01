# 100. Same Tree

### 题目描述

> 100. Same Tree

            3  
　　　　/　　　　　　　　\  
　　　　5　　　　　　　　　1  
　　/　　　　 　　　/　　　　\  
　　6　　　　2　　　0　　　　　8  
　　　　　　/　\  
　　　　　　7　4

[原题链接](https://leetcode.com/problems/same-tree/description/)

### 解题思路

将两棵树的节点按层依次放入队列，每次拿两个出来进行validation

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



