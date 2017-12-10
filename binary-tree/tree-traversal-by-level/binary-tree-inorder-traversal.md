# 94. Binary Tree Inorder Traversal

### 题目描述

> Given a binary tree, return the inorder traversal of its nodes' values.

#### Example:
Given binary tree [1,null,2,3],

```
   1
    \
     2
    /
   3
 ```

return [1,3,2].

[原题链接](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

### 解题思路

用迭代法解决二叉树通常都会考虑用stack。每次将当前节点入栈后DFS左节点。当左边节点全部进栈完毕后我们才逐个出栈并加入最终结果集可以保证中序遍历

#### Java代码实现
##### Iteration
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode walk = root;
        while (!stack.isEmpty() || walk != null) {
            if (walk != null) {
                stack.push(walk);
                walk = walk.left;
            } else {
                TreeNode node = stack.pop();
                result.add(node.val);  // Add after all left children
                walk = node.right;   
            }
        }
        return result;
    }
}
```
##### Recursion
``` java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorderTraversal(root, res);
        return res;
    }
    public void inorderTraversal(TreeNode root, List<Integer> res){
        if (root != null) {
            inorderTraversal(root.left, res);
            res.add(root.val);
            inorderTraversal(root.right, res);
        }
    }
}
```

### Reference
https://discuss.leetcode.com/topic/30632/preorder-inorder-and-postorder-iteratively-summarization