# 1038. Binary Search Tree to Greater Sum Tree

> Given the root of a binary search tree with distinct values, modify it so that every node has a new value equal to the sum of the values of the original tree that are greater than or equal to node.val.
 
#### Example 1:
![](/assets/Binary_Search_Tree_to_Greater_Sum_Tree.png)

    Input: [4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
    Output: [30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]

[原题链接](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

### 解题思路
BST + in-order traverse 可以得到递增序列
然后总list尾部开始逐次加上比自己大的节点的和

#### Java代码实现
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
    public TreeNode bstToGst(TreeNode root) {
        List<TreeNode> list = new ArrayList<>();
        inorderTraverse(root, list);
        
        if (list.size() >= 2) {
            for (int i = list.size() - 2; i >= 0; --i) {
                list.get(i).val += list.get(i + 1).val;
            }
        }

	    return root;     
    }
    
    public void inorderTraverse(TreeNode node, List<TreeNode> list) {
        if (node != null) {
            inorderTraverse(node.left, list);
            list.add(node);
            inorderTraverse(node.right, list);
            
        }
    }
}
```