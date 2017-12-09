# 144. Binary Tree Preorder Traversal

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

return [1,2,3].

[原题链接](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)

### 解题思路

和之前中序遍历稍有不同的是，每次进栈完便把当前的节点放入结果集中后才对左子树进行DFS

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode walk = root;
        while(!stack.isEmpty() || walk != null) {
            if (walk != null) {
                stack.push(walk);
                result.add(walk.val);  // Add before going to children
                walk = walk.left;
            } else {
                TreeNode node = stack.pop();
                walk = node.right;   
            }
        }
        return result;
    }
}

```

##### Recursion

```java
public class Solution {
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        // null or leaf
        if (root == null) {
            return result;
        }

        // Divide
        List<Integer> left = preorderTraversal(root.left);
        List<Integer> right = preorderTraversal(root.right);

        // Conquer
        result.add(root.val);
        result.addAll(left);
        result.addAll(right);
        return result;
    }
}
```


### Reference
https://discuss.leetcode.com/topic/30632/preorder-inorder-and-postorder-iteratively-summarization