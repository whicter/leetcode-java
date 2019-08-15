# 314. Binary Tree Vertical Order Traversal

### 题目描述

>Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).
<br> If two nodes are in the same row and column, the order should be from left to right.

#### Example 1:

    Input: [3,9,20,null,null,15,7]
    
       3
      /\
     /  \
     9  20
        /\
       /  \
      15   7 
    
    Output:
    
    [
      [9],
      [3,15],
      [20],
      [7]
    ]

#### Examples 2:

    Input: [3,9,8,4,0,1,7]
    
         3
        /\
       /  \
       9   8
      /\  /\
     /  \/  \
     4  01   7 
    
    Output:
    
    [
      [4],
      [9],
      [3,0,1],
      [8],
      [7]
    ]

#### Examples 3:

    Input: [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5)
    
         3
        /\
       /  \
       9   8
      /\  /\
     /  \/  \
     4  01   7
        /\
       /  \
       5   2
    
    Output:
    
    [
      [4],
      [9,5],
      [3,0,1],
      [8,2],
      [7]
    ]


[原题链接](https://leetcode.com/problems/binary-tree-vertical-order-traversal/)


### 解题思路
按列打印，那就在在遍历的时候计算每个节点的列数。以root为中心，作为col:0。每次有left， col --；有right，col++;
因为最后还需要将结果按col从小到大打印，所以还需要维护minCol和maxCol

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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        
        Map<Integer, List<Integer>> map = new HashMap<>(); // col -> node map
        Queue<TreeNode> q = new LinkedList<>();
        Queue<Integer> cols = new LinkedList<>();

        q.add(root); 
        cols.add(0);
        
        int minCol = 0;
        int maxCol = 0;

        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            int col = cols.poll();

            List<Integer> existingList = map.getOrDefault(col, new ArrayList<Integer>());
            existingList.add(node.val);
            map.put(col, existingList);

            if (node.left != null) {
                q.add(node.left); 
                cols.add(col - 1);
                minCol = Math.min(minCol, col - 1);
            }

            if (node.right != null) {
                q.add(node.right);
                cols.add(col + 1);
                maxCol = Math.max(maxCol, col + 1);
            }
        }

        for (int i = minCol; i <= maxCol; i++) {
            res.add(map.get(i));
        }
        return res;

    }
}
 
```