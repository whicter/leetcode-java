973. K Closest Points to Origin
### 题目描述
>We have a list of points on the plane.  Find the K closest points to the origin (0, 0). (Here, the distance between two points on a plane is the Euclidean distance.)
><br><br>You may return the answer in any order.  The answer is guaranteed to be unique (except for the order that it is in.)

 

### Example 1:

    Input: points = [[1,3],[-2,2]], K = 1
    Output: [[-2,2]]
    Explanation: 
    The distance between (1, 3) and the origin is sqrt(10).
    The distance between (-2, 2) and the origin is sqrt(8).
    Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
    We only want the closest K = 1 points from the origin, so the answer is just [[-2,2]].

### Example 2:

    Input: points = [[3,3],[5,-1],[-2,4]], K = 2
    Output: [[3,3],[-2,4]]
    (The answer [[-2,4],[3,3]] would also be accepted.)
 

**Note:**
1. <= K <= points.length <= 10000
2. -10000 < points[i][0] < 10000
3. -10000 < points[i][1] < 10000

[原题链接](https://leetcode.com/problems/k-closest-points-to-origin/)

### 解题思路
计算距离然后heap排序
- 时间复杂度
对N个节点分别做heap的插入和删除操作， 每个操作复杂度是logK, 所以整体复杂度是O(N*lgK)

- 空间复杂度
建立了一个大小为K的heap， 所以空间复杂度是O(K)

```java
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        if (points == null || points.length == 0 || K < 1){
            return points;
        }
        
        PriorityQueue<int []> pq = new PriorityQueue<>(K, (a, b) -> getDistanceSquare(b) - getDistanceSquare(a));
        for(int [] point : points){
            pq.add(point);
            if (pq.size() > K){
                pq.poll();
            }
        }
        
        int [][] res = new int[K][2];
        for (int i = 0; i < K; i++){
            res[i] = pq.poll();
        }
        
        return res;
    }
    
    private int getDistanceSquare(int [] point){
        return point[0] * point[0] + point[1] * point[1];
    }
}
```