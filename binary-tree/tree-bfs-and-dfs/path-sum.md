# 113. Path Sum II

### 题目描述

> Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.
>
>Note: A leaf is a node with no children.the root.

#### Example
Given the below binary tree and sum = 22,

            5
           / \
          4   8
         /   / \
        11  13  4
        /  \    / \
       7    2  5   1

return true, as there exist a root-to-leaf path `5 -> 4 -> 11 -> 2` which sum is 22.

[原题链接](https://leetcode.com/problems/path-sum/)

### 解题思路
比起113，这道显然容易很多，注意点仍然是循环终止条件
    

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
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        sum -= root.val;
        if (root.left == null && root.right == null) {
            return sum == 0;
        } else {
            return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
        }
    }
}
```