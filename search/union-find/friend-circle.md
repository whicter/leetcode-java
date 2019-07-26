# 547. Friend Circles

> There are **N**students in a class. Some of them are friends, while some are not. Their friendship is transitive in nature. For example, if A is a **direct** friend of B, and B is a **direct** friend of C, then A is an **indirect** friend of C. And we defined a friend circle is a group of students who are direct or indirect friends.
<br>Given a **N*N** matrix M representing the friend relationship between students in the class. If M[i][j] = 1, then the ith and jth students are **direct** friends with each other, otherwise not. And you have to output the total number of friend circles among all the students.

Example 1:

    Input: 
    [[1,1,0],
    [1,1,0],
    [0,0,1]]
    Output: 2
    Explanation:The 0th and 1st students are direct friends, so they are in a friend circle. 
    The 2nd student himself is in a friend circle. So return 2.



[原题链接](https://leetcode.com/problems/word-search/)

### 解题思路
思路一：DFS
从某个人i出发，找到第一个i的朋友；然后再从这个朋友开始继续找。每次找到新朋友需要标记一下避免重复搜索和死循环

思路二：Union Find
两层循环把共同好友union起来
然后一层循环，每次parent[i] == i的时候count++， 意味着这是一个新的集群的头

### Java代码实现-DFS：

```java
class Solution {
    public int findCircleNum(int[][] M) {
        int groupCount = 0;
        boolean[] visited = new boolean[M.length];
        for (int i = 0; i < M.length; i++) {
            if (!visited[i]) {
                dfs(M, i, visited);
                groupCount ++;
            }
        }
        return groupCount;  
    }
    
    public void dfs(int[][] M, int start, boolean[] visited) {
        for (int i = 0; i < M[0].length; i++) {
            if (M[start][i] == 1 && !visited[i]) {
                visited[i] = true;
                dfs(M, i, visited);
            }
        }
    }
}
```

### Java代码实现-Union Find
```java
class Solution {
    public int findCircleNum(int[][] M) {
        int[] parents = new int[M.length];
        for (int i = 0; i < parents.length; i++) {
            parents[i] = i;
        }
        for (int i = 0; i < M.length; i++) {
            for (int j = 0; j < M.length; j++) {
                if (M[i][j] == 1 && i != j) {
                    union(parents, i, j);
                }
            }
        }
        int count = 0;
        for (int i = 0; i < parents.length; i++) {
            if (parents[i] == i)
                count++;
        }
        return count;
    }
    
    public int find(int parent[], int i) {
        while (parent[i] != i) {
            i = parent[i];
        }
        return i;
    }

    public void union(int parent[], int x, int y) {
        int xParent = find(parent, x);
        int yParent = find(parent, y);
        if (xParent != yParent) {
            parent[yParent] = xParent;
        }
    }
}
```



