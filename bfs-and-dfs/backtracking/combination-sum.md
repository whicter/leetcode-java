# 39. Combination Sum

### 题目描述

>Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

>The same repeated number may be chosen from candidates unlimited number of times.

**Note**:
- All numbers (including target) will be positive integers.
- The solution set must not contain duplicate combinations.

#### Example 1:
    Input: candidates = [2,3,6,7], target = 7,
    A solution set is:
    [
        [7],
        [2,2,3]
    ]

#### Example 2:
    Input: candidates = [2,3,5], target = 8,
    A solution set is:
    [
        [2,2,2,2],
        [2,3,3],
        [3,5]
    ]    
[原题链接](https://leetcode.com/problems/combination-sum/)

### 解题思路

以[2, 3, 5] 为例，树形图如下：

![](/assets/Combination Sum.png)

因为数字可以重复利用，所以每个节点的子树里，可以对原数组继续递归来计算结果
在这里，我们每加入一个新数字后更新target，因此根据target状态有如下三种情况：
- target == 0: 加入结果集
- target > 0: 继续递归
- target < 0: 返回上一层

在某一层进行递归时，每一个数字都可以作为初值，因此需要for loop来循环候选数字

### Java代码实现：

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        // Arrays.sort(candidates); 
        List<List<Integer>> finalResults = new ArrayList<List<Integer>>();
        generateResults(candidates, target, finalResults, 0, new ArrayList<Integer>());
        return finalResults;
    }
    
    public void generateResults(int[] candidates, int target, List<List<Integer>> finalResults, int index, List<Integer> curRes) {
        if (target == 0) {
            finalResults.add(new ArrayList<Integer>(curRes));
        } else if (target > 0) {
            for (int i = index; i < candidates.length; i++) {
                curRes.add(candidates[i]);
                generateResults(candidates, target - candidates[i], finalResults, i, curRes); // not i + 1 because we can reuse same elements
                curRes.remove(curRes.size() - 1);
            }
        }
        
    }
}
```


