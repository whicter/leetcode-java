# 332. Reconstruct Itinerary

### 题目描述
> Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order. All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.

**Note:**

1. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
2. All airports are represented by three capital letters (IATA code).
3. You may assume all tickets form at least one valid itinerary.

#### Example 1:

    Input: [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
    Output: ["JFK", "MUC", "LHR", "SFO", "SJC"]

#### Example 2:

    Input: [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
    Output: ["JFK","ATL","JFK","SFO","ATL","SFO"]
    Explanation: Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"].
                But it is larger in lexical order.



[原题链接](https://leetcode.com/problems/reconstruct-itinerary/)

#### 解题思路
将所有的机票用数组保存起来，最后我们就是要找出一条路径将机票用完，并且如果有多条路径，就找字典序最小的。用一个hashmap<String,PriorityQueue<String>>保存每个点及其邻节点，然后使用深度遍历，第一次得到的结果便是答案（因为每次都是用的最小路径）。 另外一种方法是每次找到终点，然后删除该点继续查找下一个终点，最后得到的结果反转即可。

其实这是用来计算Euler circuit的Hierholzer’s Algorithm, 伪代码见下：
```java

path = []

DFS(u):
    While (u存在未被访问的边e(u,v))
        mark边e(u,v)为访问
        DFS(v)
    End
    path.pushLeft(u)
```   

### Java 代码实现

```java
class Solution {
    public List<String> findItinerary(List<List<String>> tickets) {
        Map<String, PriorityQueue<String>> graph = new HashMap<>();
        for (List<String> ticket : tickets) {
          graph.putIfAbsent(ticket.get(0), new PriorityQueue<>());
          graph.get(ticket.get(0)).add(ticket.get(1));
        }
        List<String> rslt = new LinkedList<>();
        dfs("JFK", graph, rslt);
        return rslt;
    }

  private void dfs(String departure, Map<String, PriorityQueue<String>> graph, List<String> rslt) {
    PriorityQueue<String> arrivals = graph.get(departure);
    while (arrivals != null && !arrivals.isEmpty()) {
      dfs(arrivals.poll(), graph, rslt);
    }
    rslt.add(0, departure);
  }
}
```



