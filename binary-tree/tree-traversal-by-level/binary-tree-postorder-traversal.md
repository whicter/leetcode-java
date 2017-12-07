# 145. Binary Tree Postorder Traversal

### 题目描述

> Given a binary tree, return the preorder traversal of its nodes' values.

#### Example:
Given binary tree [1,null,2,3],

```
   1
    \
     2
    /
   3
 ```

return [3,2,1].

[原题链接](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)

### 解题思路

http://blog.csdn.net/WangT443/article/details/51863846

#### Java代码实现
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
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> result = new LinkedList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode walk = root;
        while(!stack.isEmpty() || walk != null) {
            if (walk != null) {
                stack.push(walk);
                result.addFirst(walk.val);  // Reverse the process of preorder
                walk = walk.right;             // Reverse the process of preorder
            } else {
                TreeNode node = stack.pop();
                walk = node.left;           // Reverse the process of preorder
            }
        }
        return result;
    }
```

### Reference
https://discuss.leetcode.com/topic/30632/preorder-inorder-and-postorder-iteratively-summarization



