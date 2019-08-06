# 450. Delete Node in a BST

### 题目描述
> Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.
<br>Basically, the deletion can be divided into two stages:
<br>Search for a node to remove.
<br>If the node is found, delete the node.

**Note:** Time complexity should be O(height of tree).

### Example:

    root = [5,3,6,2,4,null,7]
    key = 3

        5
       / \
      3   6
     / \   \
    2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

        5
       / \
      4   6
     /     \
    2       7

Another valid answer is [5,2,6,null,4,null,7].

        5
       / \
      2   6
       \   \
        4   7


[原题链接](https://leetcode.com/problems/delete-node-in-a-bst/)

### 解题思路
#### 递归解法
1. 根据BST性质定位到需要删除的节点
2. 找到需要删除节点之后按子树情况讨论：
    -  如果左子树或者右子树为空（或者是叶子节点):
        <br>则用非空的子树替代被删除节点
    - 如果左右子树都不空:
        <br>根据BST的性质，只有右子树的最小节点才能成为新的根节点。因此一个简单的DFS首先找到右子树的最最左叶节点。将根节点赋值为该节点之后，再调用递归函数删除该节点

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
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return root;
        } else if (key < root.val) {
            root.left = deleteNode(root.left, key);
        } else if (key > root.val) {
            root.right = deleteNode(root.right, key);
        } else {
            // 如果某一侧为空
            if (root.left == null || root.right == null) {
                root = root.left == null ? root.right : root.left;
            } else { // 左右子树皆不为空
                TreeNode cur = root.right;

                // 找到最左下方节点
                while (cur.left != null) {
                    cur = cur.left;
                }
                // 替换节点值
                root.val = cur.val;
                // 再次递归删除当前节点
                root.right = deleteNode(root.right, cur.val);
            }
        }
        return root;
    }
}
```


#### 迭代解法：
1. 根据BST性质定位到需要删除的节点
2. 分类情况同上，难点还是在于如果被删除节点左右子树都存在的时候，新的替代者依然在被删除节点的右子树中。这时有可以分两类情况：
    - nodeToDelete.right没有左子树，那直接将nodeToDelete.right作为新的替代者，并且将nodeToDelete.left连接到自己身上
    - nodeToDelete.right有左子树，则需要找到左子树中的最左边节点，遍历过程中同时维护pre。找到后把这个节点值赋值给nodeToDelete。 然后将这个leftMost节点的右子树再赋值给pre的left即可


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
    public TreeNode deleteNode(TreeNode root, int key) {
        
        if (root == null) {
            return root;
        }
        
        if (root.val == key) {
            return removeNodeAndUpdate(root);
        }

        TreeNode cur = root, pre = null;
        while (cur != null && cur.val != key) {
            pre = cur;
            if (key < cur.val) {
                cur = cur.left;
            } else if (key > cur.val) {
                cur = cur.right;
            }
        }
        
        // key not found
        if (cur == null) {
            return root;
        }
        
        if (pre.left == cur) {
            pre.left = removeNodeAndUpdate(cur);
        } else {
            pre.right = removeNodeAndUpdate(cur);
        }
        return root;
    }
    
    private TreeNode removeNodeAndUpdate(TreeNode node) {
        if (node.left == null) {
            return node.right;
        } else if (node.right == null) {
            return node.left;
        } else {
            if (node.right.left == null) {
                TreeNode newRoot = node.right;
                newRoot.left = node.left;
                return newRoot;
            } else {
                TreeNode pre = node, cur = node.right;
                while (cur.left != null) {
                    pre = cur;
                    cur = cur.left;
                }

                node.val = cur.val;         
                pre.left = cur.right;
                return node;
            }
        }
    }
            
}
```



