## Topological Sorting

## Definition

>Topological sorting for **Directed Acyclic Graph (DAG)** is <u>a linear ordering of vertices such that for every directed edge uv, vertex u comes before v in the ordering</u>
<br>给定一个有向图，图节点的拓扑排序被定义为：
<br>对于每条有向边A--> B，则A必须排在B之前　　
拓扑排序的第一个节点可以是任何在图中没有其他节点指向它的节点　　
找到给定图的任一拓扑排序



<br>Topological Sorting for a graph is **NOT** possible if the graph is not a DAG.

## Example
![](/assets/Topological Sorting.png)
For example, a topological sorting of the following graph is “5 4 2 3 1 0”. There can be more than one topological sorting for a graph. For example, another topological sorting of the following graph is “4 5 2 3 1 0”. The first vertex in topological sorting is always a vertex with in-degree as 0 (a vertex with no in-coming edges).


## Solution
对于拓扑排序来说， 我们的中心思想是要我们可以找到一个顺序，每一次我们可以进行的工序是现在没有先序依赖的工序，按照这个顺序可以流畅的完成我们的任务。如果从图论的角度来说，实际上是从一个点遍历整个图，并且遍历图的时候，下次可以遍历的点是入度为0的点，而我们遍历的顺序就是我们所要求的拓扑排序的顺序。


那么对于一个DAG怎么求得他的拓扑序呢？
我们可以用宽度优先的方法，因为宽度优先的方法非常适合通过一点去遍历整个图。对于求拓扑排序的问题，我们宽度优先搜索有一个条件：每一次只能遍历当前入度为0的点

每次遍历一个点之后，就更新这个点相邻的点的入度信息，因为遍历了这个点，相当于相邻的点的依赖前序工序减少了1个，也就是相邻点的入度减少了1，如果相邻点中更新后有入度为0的点，那么我们就把相邻点放入到队列当中以便下一次进行访问. 具体操作如下：
- 从 DAG 图中选择一个入度为0 的顶点并输出。
- 从图中删除该顶点和所有以它为起点的有向边。
- 重复 1 和 2 直到当前的 DAG 图为空或当前图中不存在无前驱的顶点为止。后一种情况说明有向图中必然存在环。

通过这样的方法我们遍历一遍整个图。用O(m)，m为图的边数，的时间复杂度就可以求出这个图的拓扑排序解。

``` java
/**
* 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
* - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
* - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
* - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
* - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code
*/ 

/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */    
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        // Initialize map of neighbours
        ArrayList<DirectedGraphNode> result = new ArrayList<DirectedGraphNode>();
        HashMap<DirectedGraphNode, Integer> map = new HashMap();
        for (DirectedGraphNode node : graph) {
            for (DirectedGraphNode neighbor : node.neighbors) {
                map.put(neighbor, map.getOrDefault(neighbor, 0) + 1);
            }
        }

        // Initialize the queue with incoming edges = 0
        Queue<DirectedGraphNode> q = new LinkedList<DirectedGraphNode>();
        for (DirectedGraphNode node : graph) {
            if (!map.containsKey(node)) {
                q.offer(node);
                result.add(node);
            }
        }
        
        while (!q.isEmpty()) {
            DirectedGraphNode node = q.poll();
            for (DirectedGraphNode n : node.neighbors) {
                map.put(n, map.get(n) - 1);
                // all the incoming edges for the current neighbour node is resolved
                if (map.get(n) == 0) {
                    result.add(n);
                    q.offer(n);
                }
            }
        }
        return result;
    }
}
```
## Reference
http://www.geeksforgeeks.org/topological-sorting/
http://www.jiuzhang.com/solutions/topological-sorting/





