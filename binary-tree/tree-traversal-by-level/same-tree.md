# 100. Same Tree

### 题目描述

> Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.


Example 1:

Input:
```
           1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]
 ```

Output: true
Example 2:

Input:
           1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
Example 3:

Input: 
           1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false

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



