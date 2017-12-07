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
为了保证不丢失根节点信息，所以依然会将当前节点加入结果集后再做DFS。但是为了保证是后序，所以结果集是用LinkedList而非ArrayList来储存结果——每次将节点加在第一位。也正因为如此，进栈的节点变为右子树而非左子树。简单流程如下所示：
    step 1: root
    step 2: right -> root
    step 3: left -> root

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



