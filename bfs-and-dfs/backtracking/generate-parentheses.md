# 22. Generate Parentheses

### 题目描述

> Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

> For example, given n = 3, a solution set is:

    [
        "((()))",
        "(()())",
        "(())()",
        "()(())",
        "()()()"
    ]


[原题链接](https://leetcode.com/problems/generate-parentheses/)

### 解题思路

n = 1: LR
n = 2: L LR R, LR LR
n = 3: .....

无法推出线性关系，无可扩展性，属于树形问题，考虑递归 + 回溯

n = 3的树形图如下：
原始问题的变量-> 站在顶点的时候：L， leftCount, rightCount, 
![](/assets/GenerateParentheses_n=3.png)

可以发现，节点有如下几种状态

1. 没有孩子：
depth == 2n - 1

2. 只能有右孩子：
leftCount == n

3. 只有左孩子
rightCount == leftCount
rightCount不能大于leftCount

4. else

对于初始状态，即原始问题的变量 -> 站在顶点的时候：L， leftCount, rightCount, 

### Java代码实现：

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> results = new ArrayList<>();
        
        addResult(n, results, new StringBuilder(), 1, 0, '(') ;
        return results; 
    }
    private void addResult(int n, List<String> finalResults, StringBuilder curRes, int leftCount, int rightCount, char bracket) {
        curRes.append(bracket);
        if (curRes == 2 * n) {
            finalResults.add(curRes.toString());
            return;
        }
        if (leftCount == n) {
            addResult(n, finalResults, curRes, leftCount, rightCount + 1, ')');
        } else if (rightCount == leftCount) {
            addResult(n, finalResults, curRes, leftCount + 1, rightCount, '(');
        } else {
            addResult(n, finalResults, curRes, leftCount + 1, rightCount, '(');
            curRes.deleteCharAt(curRes.length() - 1);
            addResult(n, finalResults, curRes, leftCount, rightCount + 1, ')');;
        }
        
        curRes.deleteCharAt(curRes.length() - 1);
    }
}
```

进一步分析发现，对于递归，有三类操作：hasLeft -> processLeft，hasRight -> processRight，hasNothing -> processNothing。而上述的四种状态存在可以合并的case：
hasLeft: 
- leftCount < n

hasRight:
- rightCount < leftCount

### 代码简化为：
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> results = new ArrayList<>();
        StringBuilder path = new StringBuilder();
        addResult('(', 1, 0, n, results, path) ;
        return results; 
    }
    private void addResult(char a, int leftCount, int rightCount, int n, List<String> result, StringBuilder path) {
        
        path.append(a);
        
        if (leftCount + rightCount - 1 == 2 * n - 1) {
            result.add(path.toString());
        }
        
        if (leftCount < n) {
            addResult('(', leftCount + 1, rightCount, n, result, path);
        } 
        if (leftCount > rightCount) {
            addResult(')', leftCount, rightCount + 1, n, result, path);
        }
        
        path.deleteCharAt(path.length() - 1);
    }
}
```



