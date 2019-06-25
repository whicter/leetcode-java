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

Return:

    [
        [5,4,11,2],
        [5,8,4,5]
    ]

[原题链接](https://leetcode.com/problems/path-sum-ii/)

### 解题思路
解法基本类同其他的DFS / Backtracking的题

需要注意的是循环的终结条件，即：只有当前节点为叶子节点且sum为目标和的时候才加入结果集
    

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
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> finalResult = new ArrayList<>();
        addPathSum(root, sum, finalResult, new ArrayList<Integer>());
        return finalResult;
    }
    private void addPathSum(TreeNode curNode, int sum, List<List<Integer>> finalResult, List<Integer> curResult) {
        if (curNode != null) {
            
            curResult.add(curNode.val);
            sum -= curNode.val;
            
            // Only add the temp path to the result when the current node is leaf node
            if (curNode.left == null && curNode.right == null && sum == 0) {
                finalResult.add(new ArrayList<Integer>(curResult));
            } else {
                addPathSum(curNode.left, sum, finalResult, curResult);
                addPathSum(curNode.right, sum, finalResult, curResult);
            } 
            
            curResult.remove(curResult.size() - 1);
        }
    }
}
```