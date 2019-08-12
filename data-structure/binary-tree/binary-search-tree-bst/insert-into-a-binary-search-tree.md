# 701. Insert into a Binary Search Tree

>Given the root node of a binary search tree (BST) and a value to be inserted into the tree, insert the value into the BST. Return the root node of the BST after the insertion. It is guaranteed that the new value does not exist in the original BST.
<br>Note that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return any of them.

### Example

Given the tree:

            4
           / \
          2   7
         / \
        1   3
And the value to insert: 5
You can return this binary search tree:

         4
       /   \
      2     7
     / \   /
    1   3 5
This tree is also valid:

         5
       /   \
      2     7
     / \   
    1   3
         \
          4




[原题链接](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

### 解题思路
#### 递归解法
根据BST性质每一轮判断目标节点是需要在左边递归还是右边递归。终止条件是当递归到最后一个叶子节点的时候，生成新节点

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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }

        if (val > root.val) {
            root.right = insertIntoBST(root.right, val); // insert into the right subtree
        } else {
            root.left = insertIntoBST(root.left, val); // insert into the left subtree
        }
        return root;
    }
}
```


#### 迭代解法：
一样的思路。 需要注意的是，在每次判断完决定走哪一侧之前先判断是否该侧子树已空。如果已空，那直接生成新节点而后返回根节点即可


```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        TreeNode cur = root;
        
        while (cur != null) {
            if (val > cur.val) {
                if (cur.right == null) {
                    cur.right = new TreeNode(val);
                    return root;
                } else {
                    cur = cur.right;
                }
            } else {
                if (cur.left == null) {
                    cur.left = new TreeNode(val);
                    return root;
                } else {
                    cur = cur.left;
                }
            }
        }
        return new TreeNode(val);
        
    }
}
```



