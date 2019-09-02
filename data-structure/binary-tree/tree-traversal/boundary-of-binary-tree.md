# 545. Boundary of Binary Tree

### 题目描述

>Given a binary tree, return the values of its boundary in anti-clockwise direction starting from root. Boundary includes left boundary, leaves, and right boundary in order without duplicate nodes. (The values of the nodes may still be duplicates.)

Left boundary is defined as the path from root to the left-most node. Right boundary is defined as the path from root to the right-most node. If the root doesn't have left subtree or right subtree, then the root itself is left boundary or right boundary. Note this definition only applies to the input binary tree, and not applies to any subtrees.

The left-most node is defined as a leaf node you could reach when you always firstly travel to the left subtree if exists. If not, travel to the right subtree. Repeat until you reach a leaf node.

The right-most node is also defined by the same way with left and right exchanged.

#### Example 1

    Input:
       1
        \
         2
        / \
       3   4

    Ouput:
    [1, 3, 4, 2]

    Explanation:
    The root doesn't have left subtree, so the root itself is left boundary.
    The leaves are node 3 and 4.
    The right boundary are node 1,2,4. Note the anti-clockwise direction means you should output reversed right boundary.
    So order them in anti-clockwise without duplicates and we have [1,3,4,2].

#### Example 2

    Input:
            ____1_____
           /          \
          2            3
         / \          / 
        4   5        6   
       / \          / \
      7   8        9  10  
        
    Ouput:
    [1,2,4,7,8,9,10,6,3]

    Explanation:
    The left boundary are node 1,2,4. (4 is the left-most node according to definition)
    The leaves are node 4,7,8,9,10.
    The right boundary are node 1,3,6,10. (10 is the right-most node).
    So order them in anti-clockwise without duplicate nodes we have [1,2,4,7,8,9,10,6,3].

 


[原题链接](https://leetcode.com/problems/boundary-of-binary-tree/)


### 解题思路
对于每一个**root的左子树**节点(除了root.left)来说：
- 如果parent是boundary且自己是left child，那自己也是boundary
- 如果parent是boundary且自己是right child，那只有当parent没有left child时，自己才是boundary
- 如果自己是leaf节点，那自己也是boundary


对于每一个**root的右子树**(除了root.right)节点来说：
- 如果parent是boundary且自己是right child，那自己也是boundary
- 如果parent是boundary且自己是left child，那只有当parent没有right child时，自己才是boundary
- 如果自己是leaf节点，那自己也是boundary

对于右子树，还需要注意的是在递归完自己的children后才加入自己

####  Java代码实现

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
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        List<Integer> boundary = new ArrayList<>();
        if (root != null) {
            boundary.add(root.val);
            boundary.addAll(getLeftPart(root.left, new ArrayList<>(), true));
            boundary.addAll(getRightPart(root.right, new ArrayList<>(), true));
        }
        return boundary;
    }

    private List<Integer> getLeftPart(TreeNode node, List<Integer> leftPart, boolean isBoundary) {
        if (node != null) {
            if (isBoundary || isLeaf(node)) {
                leftPart.add(node.val);
            }
            getLeftPart(node.left, leftPart, isBoundary);
            getLeftPart(node.right, leftPart, (isBoundary && (node.left == null)));
        }
        return leftPart;
    }

    private List<Integer> getRightPart(TreeNode node, List<Integer> rightPart, boolean isBoundary) {
        if (node != null) {
            getRightPart(node.left, rightPart, (isBoundary && (node.right == null)));
            getRightPart(node.right, rightPart, isBoundary);
            if (isBoundary || isLeaf(node)) {
                rightPart.add(node.val);
            }
            
        }
        return rightPart;
    }

    private boolean isLeaf(TreeNode node) {
        return node != null && node.left == null && node.right == null;
    }
}
 
```