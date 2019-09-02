# 207. Course Schedule

### 题目描述

>There are a total of n courses you have to take, labeled from 0 to n-1.
<br><br>Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]
<br><br>Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

#### Example 1:

    Input: 2, [[1,0]] 
    Output: true
    Explanation: There are a total of 2 courses to take. 
                 To take course 1 you should have finished course 0. So it is possible.

#### Example 2:

    Input: 2, [[1,0],[0,1]]
    Output: false
    Explanation: There are a total of 2 courses to take. 
                 To take course 1 you should have finished course 0, and to take course 0 you should
                 also have finished course 1. So it is impossible.


[原题链接](https://leetcode.com/problems/course-schedule/)



### 解题思路
典型的拓扑排序。遍历所有的pair构造parent -> children map，同时维护一个indegree的数组来维护入度

初始化后将入度为0的节点放入queue。然后遍历children，每个children被遍历一次相应的入度也➖1。入度为0后也放入queue

最后比较遍历结果的count是否和总课数相等

#### Java代码实现

``` java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[] indegrees = new int[numCourses];
        Map<Integer, Set<Integer>> childrenMap = new HashMap<>();
        
        for (int[] entry : prerequisites) {
            Set<Integer> curPrerequisites = childrenMap.get(entry[1]);
            if (null == curPrerequisites) {
                curPrerequisites = new HashSet<Integer>();
            }
            
            curPrerequisites.add(entry[0]);
            childrenMap.put(entry[1], curPrerequisites);
            
            indegrees[entry[0]] ++;
        }
        
        Queue<Integer> queue = new LinkedList<>();
        
        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] == 0) {
                queue.add(i);
            }
        }
        
        int count = 0;
        while (!queue.isEmpty()) {
            int cur = queue.poll();
            count ++;
            
            Set<Integer> children = childrenMap.get(cur);
            if (children != null) {
                for (int child : children) {
                    indegrees[child]--;
                    if (indegrees[child] == 0) {
                        queue.add(child);
                    }
                }
            }
        }
        return count == numCourses;
        
    }
}
```