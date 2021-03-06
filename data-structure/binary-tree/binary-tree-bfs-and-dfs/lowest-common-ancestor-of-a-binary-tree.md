# 236. Lowest Common Ancestor of a Binary Tree

### 题目描述

> Given a binary tree, find the lowest common ancestor \(LCA\) of two given nodes in the tree.  
> According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants \(where we allow a node to be a descendant of itself\).”
>
> For example, the lowest common ancestor \(LCA\) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

![](/assets/Lowest Common Ancestor of a Binary Tree.png)    

### Example 1:

    Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
    Output: 3
    Explanation: The LCA of nodes 5 and 1 is 3.

### Example 2:

    Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
    Output: 5
    Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.     

[原题链接](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)

### 解题思路

#### 1.递归

既然是递归，那最重要的必然就是递归的终止条件。  
    (a) 如果正处于递归中的节点为空，那直接返回即可。  
    (b) 如果正处于递归中的节点是目标节点之一，我们也可以终止递归并将信息返回给caller。如果左右递归的结果分别包含两个目标节点，那caller节点就是所求结果；如果有一处为空，那就将这信息继续往上一层传递。

最终的如果我们从一个big picture来看，对根节点的左右子树分别递归，如果根节点左右递归的结果分别包含两个目标节点，根节点节点就是所求结果；如果一处为空，那结果必定在另一侧

![](/assets/LCA.png)
如上图中我们要查找节点4,3的最小公共父节点，那么上述代码的执行过程如下

- 判断1是否4,3节点：不是，则查询1的左子树和右子树
- 1的左子树中先判断2是否4,3节点：不是，查找2的左右子树 
- 2的左子树 显然返回结果4；2的右子树返回结果null，显然2的左右子树并没有都返回树中的节点，因此2不是4,3的最小公共父节点，因此以2位根节点的1的左子树调用方法返回的是4。
- 1的右子树判断3节点是否是4,3节点：发现是的，直接返回3节点。
- 1的左右子树的递归调用都返回了结果，因此1就是节点4,3的最小公共父节点。

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

        TreeNode candidate_1 = lowestCommonAncestor(root.left, p, q);
        TreeNode candidata_2 = lowestCommonAncestor(root.right, p, q);

        if (candidate_1 == null) return candidata_2;
        if (candidata_2 == null) return candidate_1;

        return root;
    }
}
```

#### 2.迭代 with two stacks.

找到两条路径后分别做pop操作
需要注意的是，stack是node to root, 即root在stack最上。
每次pop之后比较是否相同，直到最后一次相同的时候，就是LCA

#### Java代码实现

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        Stack<TreeNode> stackP = new Stack<TreeNode>();
        Stack<TreeNode> stackQ = new Stack<TreeNode>();
        
        findNodeToRootPath(root, p, stackP);
        findNodeToRootPath(root, q, stackQ);
        
        TreeNode target = root;
        TreeNode temp;
        
        System.out.println(stackP.peek().val + " " + stackQ.peek().val);
        
        while (!stackP.isEmpty() && !stackQ.isEmpty()){
            temp = stackP.pop();
            
            if (temp == stackQ.pop()) {
                target = temp;
            } else {
                break; 
            }
            
        }
        return target;
    }

    public boolean findNodeToRootPath(TreeNode root, TreeNode p, Stack<TreeNode> s) {
        if (root == null) {
            return false;
        }
        
        if (root == p) {
            s.push(root);
            return true;
            
        } else if (findNodeToRootPath(root.left, p, s) || findNodeToRootPath(root.right, p, s)) {
            s.push(root);
            return true;
            
        } else {
            return false;
        }
    }
}
```