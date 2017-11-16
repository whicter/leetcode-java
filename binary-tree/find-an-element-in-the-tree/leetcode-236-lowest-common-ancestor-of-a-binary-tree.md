# Lowest Common Ancestor of a Binary Tree

### 题目描述

> Given a binary tree, find the lowest common ancestor \(LCA\) of two given nodes in the tree.  
> According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants \(where we allow a node to be a descendant of itself\).”
>
> For example, the lowest common ancestor \(LCA\) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

            3  
　　　　/　　　　　　　　\  
　　　　5　　　　　　　　　1  
　　/　　　　 　　　/　　　　\  
　　6　　　　2　　　0　　　　　8  
　　　　　　/　\  
　　　　　　7　4

[原题链接](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)

### 解题思路

#### 1.递归

既然是递归，那最重要的必然就是递归的终止条件。  
   \(a\) 如果正处于递归中的节点为空，那直接返回即可。  
   \(b\) 如果正处于递归中的节点是目标节点之一，我们也可以终止递归并将信息返回给caller。如果左右递归的结果分别包含两个目标节点，那caller节点就是所求结果；如果有一处为空，那就将这信息继续往上一层传递。

最终的如果我们从一个big picture来看，对根节点的左右子树分别递归，如果根节点左右递归的结果分别包含两个目标节点，根节点节点就是所求结果；如果一处为空，那结果必定在另一侧

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }

        if (root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        return left != null && right != null ? root : left == null ? right : left; 
    }
}
```

#### 2.迭代 with two stacks.

相当于暴力解法了，找到两条路径后分别做pop操作

#### Java代码实现

```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        Stack<TreeNode> sp = new Stack<TreeNode>();
        Stack<TreeNode> sq = new Stack<TreeNode>();
        findNode(root, p, sp);
        findNode(root, q, sq);
        TreeNode target = root;
        TreeNode temp;
        while (!sp.isEmpty() && !sq.isEmpty()){
            temp = sp.pop();
            if (temp == sq.pop()) {
                target = temp;
            }
            else {
                break;
            }
        }
        return target;
    }

    public boolean findNode(TreeNode root, TreeNode p, Stack<TreeNode> s) {
        if (root == null) {
            return false;
        }
        if (root == p) {
            s.push(root);
            return true;
        } else if (findNode(root.left, p, s) || findNode(root.right, p,s)) {
            s.push(root);
            return true;
        } else{
            return false;
        }
    }
}
```



