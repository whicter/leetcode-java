# 199. Binary Tree Right Side View

### 题目描述
>Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

#### Example:

    Input: [1,2,3,null,5,null,4]
    Output: [1, 3, 4]
    Explanation:
    
       1            <---
     /   \
    2     3         <---
     \     \
      5     4       <---


[原题链接](https://leetcode.com/problems/binary-tree-right-side-view/)

### 解题思路
BFS按行遍历，固定queue的size然后只放入最后一个节点

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list = new LinkedList<Integer>();
        if (root == null) {
            return list;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size;i++) {
                TreeNode node = queue.poll();
                if (i == size - 1) {
                    list.add(node.val);
                }
                offerNode(node.left, queue);
                offerNode(node.right, queue);
            }
        }
        return list;
    }
    
    private void offerNode(TreeNode node, Queue<TreeNode> queue) {
        if (node != null) {
            queue.offer(node);
        }
    }
}
```



