# 297. Serialize and Deserialize Binary Tree
### 题目描述

>Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.
<br>
Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.


#### Example
For example, you may serialize the following tree

        1
       / \
      2   3
         / \
        4   5

as <span style="background-color:#ffe6e6"><font color=#cc0000 >"[1,2,3,null,null,4,5]"</font></span>


[原题链接](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)


### 解题思路
没什么花头，Queue解决战斗。稍微需要注意的是，在deserialize的时候每次拿出两个节点

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
public class Codec {

    private String delimiter =  ",";
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) {
            return "";
        }
    
        Queue<TreeNode> queue = new LinkedList<>();
        StringBuilder res = new StringBuilder();
        queue.add(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            if (node == null) {
                res.append("null");
            } else {
                res.append(node.val );
                queue.add(node.left);
                queue.add(node.right);
            }
            res.append(delimiter);
        }
        res.deleteCharAt(res.length() - 1);
        return res.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (null == data || data == "") {
            return null;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        String[] values = data.split(delimiter);
        TreeNode root = new TreeNode(Integer.parseInt(values[0]));
        queue.add(root);
        for (int i = 1; i < values.length; i++) {
            TreeNode parent = queue.poll();
            if (!values[i].equals("null")) {
                TreeNode left = new TreeNode(Integer.parseInt(values[i]));
                parent.left = left;
                queue.add(left);
            }
            if (!values[++i].equals("null")) {
                TreeNode right = new TreeNode(Integer.parseInt(values[i]));
                parent.right = right;
                queue.add(right);
            }
        }
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```