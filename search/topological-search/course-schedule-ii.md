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
和[207. Course Schedule](search/topological-search/course-schedule.md) 一样的思路，只是增加一个数组用来返回结果

#### Java代码实现

``` java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {

        Map<Integer, Set<Integer>> children = new HashMap<>();
        int[] indegrees = new int[numCourses];
        int[] topologicalOrder = new int[numCourses];

        // Create the adjacency list representation of the graph
        for (int[] entry : prerequisites) {
            Set<Integer> curChildren = children.getOrDefault(entry[1], new HashSet<Integer>());
            curChildren.add(entry[0]);
            children.put(entry[1], curChildren);

            // Record in-degree of each vertex
            indegrees[entry[0]] ++;
        }

        // Add all vertices with 0 in-degree to the queue
        Queue<Integer> q = new LinkedList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] == 0) {
                q.add(i);
            }
        }

        int totalCount = 0;
        // Process until the Q becomes empty
        while (!q.isEmpty()) {
            int node = q.poll();
            topologicalOrder[totalCount++] = node;

            // Reduce the in-degree of each child by 1
            if (children.containsKey(node)) {
                for (Integer child : children.get(node)) {
                    indegrees[child]--;

                    // If in-degree of a child becomes 0, add it to the Q
                    if (indegrees[child] == 0) {
                        q.add(child);
                    }
                }
            }
        }

        // Check to see if topological sort is possible or not.
        if (totalCount == numCourses) {
            return topologicalOrder;
        }

        return new int[0];
    }
}
```