# 129. Sum Root to Leaf Numbers

### 题目描述

> Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.
>
>An example is the root-to-leaf path 1->2->3 which represents the number 123.
>
>Find the total sum of all root-to-leaf numbers.



#### Example1:

    Input: [1,2,3]
        1
       / \
      2   3
    Output: 25
    Explanation:
    The root-to-leaf path 1->2 represents the number 12.
    The root-to-leaf path 1->3 represents the number 13.
    Therefore, sum = 12 + 13 = 25.

#### Example 2:

    Input: [4,9,0,5,1]
        4
       / \
      9   0
     / \
    5   1
    Output: 1026
    Explanation:
    The root-to-leaf path 4->9->5 represents the number 495.
    The root-to-leaf path 4->9->1 represents the number 491.
    The root-to-leaf path 4->0 represents the number 40.
    Therefore, sum = 495 + 491 + 40 = 1026.

[原题链接](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

### 解题思路
对于每个顶点，把自己的parent * 10 加上自己传到下一层
通过递归获取当前层的和
    

#### Java代码实现

```java
class Solution {
    public int sumNumbers(TreeNode root) {
        return dfs(root, 0);
    }

    private int dfs(TreeNode root, int prev){
        if (root == null) {
            return 0;
        }

        int sum = root.val + prev * 10;
        if (root.left == null && root.right == null) {
            return sum;
        }

        return dfs(root.left, sum) + dfs(root.right, sum);
    }
}
```