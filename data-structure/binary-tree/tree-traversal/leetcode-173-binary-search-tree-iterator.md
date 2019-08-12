# 173. Binary Search Tree Iterator

### 题目描述

>Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

>Calling next() will return the next smallest number in the BST.


#### Example
![](/assets/bst-iterator.png)

    BSTIterator iterator = new BSTIterator(root);
    iterator.next();    // return 3
    iterator.next();    // return 7
    iterator.hasNext(); // return true
    iterator.next();    // return 9
    iterator.hasNext(); // return true
    iterator.next();    // return 15
    iterator.hasNext(); // return true
    iterator.next();    // return 20
    iterator.hasNext(); // return false

[原题链接](https://leetcode.com/problems/binary-search-tree-iterator/)


### 解题思路
每次都要打印最小值，又是BST，很自然的想到inorder traversal

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
class BSTIterator {

    private List<Integer> nodesList;
    private int idx = 0;
    
    public BSTIterator(TreeNode root) {
        List<Integer> nodesList = new ArrayList<>();
        inorderTraversal(root, nodesList);
        this.nodesList = nodesList;
    }
    
    /** @return the next smallest number */
    public int next() {
        return nodesList.get(idx++);
        
    }
    
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return idx < nodesList.size();
        
    }
    
    private void inorderTraversal(TreeNode root, List<Integer> nodesList) {
        if (root != null) {
            inorderTraversal(root.left, nodesList);
            nodesList.add(root.val);
            inorderTraversal(root.right, nodesList);
        }
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
 
```