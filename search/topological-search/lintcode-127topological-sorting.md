# 127 Topological Sorting

### 题目描述

>Given an directed graph, a topological order of the graph nodes is defined as follow:
    * For each directed edge A -> B in graph, A must before B in the order list.
    * The first node in the order can be any node in the graph with no nodes direct to it.
    
> Find any topological order for the given graph.

#### Example 1:

    Input: graph = {0,1,2,3#1,4#2,4,5#3,4,5#4#5}
    Output: [0, 1, 2, 3, 4, 5]
    Explanation: The topological order can be:
                [0, 1, 2, 3, 4, 5]
                [0, 2, 3, 1, 5, 4]
![](/assets/toplogical_sort.jpeg)
[原题链接](https://www.lintcode.com/problem/127/)



### 解题思路
拓扑排序，adjacency map 来确定入度

#### Java代码实现

``` java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     List<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) {
 *         label = x;
 *         neighbors = new ArrayList<DirectedGraphNode>();
 *     }
 * }
 */

public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        // write your code here

        ArrayList<DirectedGraphNode> order = new ArrayList<>();
        Map<DirectedGraphNode, Integer> indgreeMap = new HashMap<>();

        for (DirectedGraphNode node : graph) {
            for (DirectedGraphNode neighbor : node.neighbors) {
                if (indgreeMap.containsKey(neighbor)) {
                    indgreeMap.put(neighbor, indgreeMap.get(neighbor) + 1);
                } else {
                    indgreeMap.put(neighbor, 1);
                }
            }
        }

        // Initialize queue with 0 indegree nodes;
        Queue<DirectedGraphNode> queue = new ArrayDeque<>();
        for (DirectedGraphNode node : graph) {
            if (!indgreeMap.containsKey(node)) {
                queue.offer(node);
                order.add(node);
            }
        }

        while (!queue.isEmpty()) {
            DirectedGraphNode node = queue.poll();
            for (DirectedGraphNode neighbor : node.neighbors) {
                indgreeMap.put(neighbor, indgreeMap.get(neighbor) - 1);
                if (indgreeMap.get(neighbor) == 0) {
                    order.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }
        
        return order;
    }
}
```