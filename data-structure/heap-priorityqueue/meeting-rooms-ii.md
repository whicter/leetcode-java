# 253. Meeting Rooms II
### 题目描述
>Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...] (si < ei)`, find the minimum number of conference rooms required.

#### Example 1:

    Input: [[0, 30],[5, 10],[15, 20]]
    Output: 2

#### Example 2:

    Input: [[7,10],[2,4]]
    Output: 1

**NOTE: **input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

[原题链接](https://leetcode.com/problems/meeting-rooms-ii/)

### 解题思路
用堆来管理房间的结束时间, 在循环的时候判断：
- 如果当前时间段的开始时间大于最早结束的时间，则可以更新这个最早的结束时间为当前时间段的结束时.
- 如果小于的话，就加入一个新的结束时间，表示新的房间

### 复杂度
时间 O(NlogN) 空间 O(N)

#### Java代码实现
```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if (intervals.length == 0) return 0;
        
        Arrays.sort(intervals, (o1, o2) -> Integer.compare(o1[0], o2[0]));
        
        // 用堆来管理房间的结束时间
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        pq.offer(intervals[0][1]); // end time of first meeting
        
        int result = 1;
        // 如果当前时间段的开始时间大于最早结束的时间，则可以更新这个最早的结束时间为当前时间段的结束时.
        // 如果小于的话，就加入一个新的结束时间，表示新的房间
        for (int i = 1; i < intervals.length; i++) {
            int[] interval = intervals[i];
            if (interval[0] >= pq.peek()) {
                pq.poll();
            }
            pq.offer(interval[1]);
        }
        
        // 有多少结束时间就有多少房间
        return pq.size();
    }
}
```