# 366. Find Leaves of Binary Tree   

### 题目描述
>Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is empty.


### Example:
    Input: [1,2,3,4,5]
    
            1
            / \
            2   3
        / \     
        4   5    

    Output: [[4,5,3],[2],[1]]

### Explanation:

1. Removing the leaves [4,5,3] would result in this tree:

          1
         / 
        2          
 

2. Now removing the leaf [2] would result in this tree:

          1          
 

3. Now removing the leaf [1] would result in the empty tree:

          []         




[原题链接](https://leetcode.com/problems/find-leaves-of-binary-tree/)

### 解题思路
对于每个节点进行DFS的时候，求出该节点到其叶子节点的最大深度，这样就能放入对应的list中

#### Java代码实现-DFS：

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
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        
        dfsHeight(root, result);
        return result;
    }
    private int dfsHeight(TreeNode node, List<List<Integer>> result) {
        if (node == null) {
            return 0;
        }

        int left_d = dfsHeight(node.left, result);
        int right_d = dfsHeight(node.right, result);
        
        // find the max depth from the current node to its leaf
        // need to have the +1 o dynamically increating the result size
        int level = Math.max(left_d, right_d) + 1; 
        
        if (level > result.size()) {
            result.add(new ArrayList<>());
        }
        
        result.get(level - 1).add(node.val);
        
        // System.out.println("TreeNode val: " + node.val);
        // System.out.println(level);
        
        return level;
    }
}
```


