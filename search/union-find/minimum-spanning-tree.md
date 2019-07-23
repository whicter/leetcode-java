# 629. Minimum Spanning Tree

### 题目描述

>IGiven a list of Connections, which is the Connection class (the city name at both ends of the edge and a cost between them), find edges that can connect all the cities and spend the least amount.
Return the connects if can connect all the cities, otherwise return empty list.

### Example 1:

    Input:
    ["Acity","Bcity",1]
    ["Acity","Ccity",2]
    ["Bcity","Ccity",3]
    Output:
    ["Acity","Bcity",1]
    ["Acity","Ccity",2]

### Example 2:
    Input:
    ["Acity","Bcity",2]
    ["Bcity","Dcity",5]
    ["Acity","Dcity",4]
    ["Ccity","Ecity",1]
    Output:
    []

    Explanation:
    No way


[原题链接](https://www.lintcode.com/problem/minimum-spanning-tree/description)



### 解题思路
1. 最小生成树， 就是在图上取一些边，使得整个树不存在环
2. 这里采用Kruskal算法，就是先排序，每次都从成本最小的开始选，如果不会够成环，就加到结果里面去，判断环的地方，用union find算法
3. 直到遍历到够了（也就是边的个数=节点个数-1）。



### Java代码实现

``` java
/**
 * Definition for a Connection.
 * public class Connection {
 *   public String city1, city2;
 *   public int cost;
 *   public Connection(String city1, String city2, int cost) {
 *       this.city1 = city1;
 *       this.city2 = city2;
 *       this.cost = cost;
 *   }
 * }
 */

public class Solution {
    /**
     * @param connections given a list of connections include two cities and cost
     * @return a list of connections from results
     */
    
    public List<Connection> lowestCost(List<Connection> connections) {
        HashMap<String, Integer> cities = new HashMap<String, Integer>();
        List<Connection> result = new ArrayList<Connection>();
        int[] parents;
        int citiesCount = 0;
        
        // Sort based on costs
        for (Connection connect : connections) {
            if (!cities.containsKey(connect.city1)) {
                cities.put(connect.city1, citiesCount++);
            }
            if (!cities.containsKey(connect.city2)) {
                cities.put(connect.city2, citiesCount++);
            }
        }
        
        Comparator<Connection> comparator = new Comparator<Connection>() {
            public int compare(Connection a, Connection b) {
                if (a.cost != b.cost) {
                    return a.cost - b.cost;
                }
                if (!a.city1.equals(b.city1)) {
                    return a.city1.compareTo(b.city1);
                }
                return a.city2.compareTo(b.city2);
            }
        };
        Collections.sort(connections, comparator);
        
        // Union Find
        parents = new int[citiesCount];
        for (int i = 0; i < parents.length; i++) {
            parents[i] = i;
        }
        
        for (Connection connect : connections) {
            int idx1 = cities.get(connect.city1);
            int idx2 = cities.get(connect.city2);
            
            int parent1 = find(parents, idx1);
            int parent2 = find(parents, idx2);
            
            if (parent1 != parent2) {
                parents[parent1] = parent2;
                result.add(connect);
            }
        }
        
        return (result.size() == citiesCount - 1) ? result : new ArrayList<Connection>();
    }
    
    private int find(int[] parents, int idx) {
        while (parents[idx] != idx) {
            // parents[idx] = parents[parents[idx]];
            // not necessary
            idx = parents[idx];
        }
        
        return idx;
    }
}
```