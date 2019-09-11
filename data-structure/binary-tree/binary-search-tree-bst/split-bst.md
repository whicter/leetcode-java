# 776. Split BST

### 题目描述
> Given a Binary Search Tree (BST) with root node root, and a target value V, split the tree into two subtrees where one subtree has nodes that are all smaller or equal to the target value, while the other subtree has all nodes that are greater than the target value.  It's not necessarily the case that the tree contains a node with value V.
>
> Additionally, most of the structure of the original tree should remain.  Formally, for any child C with parent P in the original tree, if they are both in the same subtree after the split, then node C should still have the parent P.
>
> You should output the root TreeNode of both subtrees after splitting, in any order.

Example 1:

    Input: root = [4,2,6,1,3,5,7], V = 2
    Output: [[2,1],[4,3,6,null,null,5,7]]
    Explanation:
    Note that root, output[0], and output[1] are TreeNode objects, not arrays.
    
    The given tree [4,2,6,1,3,5,7] is represented by the following diagram:
    
              4
            /   \
          2      6
         / \    / \
        1   3  5   7
    
    while the diagrams for the outputs are:
    
              4
            /   \
          3      6      and    2
                / \           /
               5   7         1

**Note:**
- The size of the BST will not exceed 50.
-The BST is always valid and each node's value is different.


[原题链接](https://leetcode.com/problems/split-bst/)

### 解题思路
通过观察我们首先发现，无论如何，root总是会包含在最终的返回结果中。根据BST的性质，如果root的值比V大，那么root以及其右子树的结构都无需变化，切分只发生在root的左子树中。

需要注意的是，root的左子树中也有可能存在比V大的分支，因此切分完，需要将新节点的右子树接回root成为root新的左子树

可以发现对root的左子树进行分割的思路和对root的分割完全一样，因此可以用递归来实现对root左子树的切割

root的值小于等于V的情况可以镜像处理。

#### Java代码实现

```java
class Solution {
    public TreeNode[] splitBST(TreeNode root, int V) {
        if (root == null) {
            return new TreeNode[]{null, null};
        } else if (root.val <= V) {
            TreeNode[] rightSplit = splitBST(root.right, V);
            root.right = rightSplit[0];
            rightSplit[0] = root;
            return rightSplit;
        } else {
            TreeNode[] leftSplit = splitBST(root.left, V);
            root.left = leftSplit[1];
            leftSplit[1] = root;
            return leftSplit;
        }
    }
}

```



    