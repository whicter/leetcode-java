# 57. Insert Interval
### 题目描述

>Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).
<br>You may assume that the intervals were initially sorted according to their start times.

#### Example 1
>Given <span style="background-color:#ffe6e6"><font color=#cc0000 >[1, 3], [6, 9]</font></span>, insert and merge <span style="background-color:#ffe6e6"><font color=#cc0000 >[2, 5]</font></span> in as <span style="background-color:#ffe6e6"><font color=#cc0000 >[1, 5], [6, 9]</font></span>.  

#### Example 2
>Given <span style="background-color:#ffe6e6"><font color=#cc0000 >[1,2], [3, 5], [6, 7], [8, 10], [12, 16]</font></span>, insert and merge <span style="background-color:#ffe6e6"><font color=#cc0000 >[4, 9]</font></span> in as <span style="background-color:#ffe6e6"><font color=#cc0000 >[1, 2], [3, 10], [12, 16]</font></span>.  


[原题链接](https://leetcode.com/problems/insert-interval/description/)

### 解题思路
不是很明白为什么这道题居然还是hard难度。题设里原有的区间不会重叠，所以就非常好办，一共有两大类情况：

1. 当前区间和所需要插入区间完全不重叠
   <br>这时候又分为两个子case：
        - 当前区间在新区间之前
        那只需要把当前区间放入结果集即可
        - 当前区间在新区间之后
        那需要将新区间加入结果集之后再加入当前区间
2. 当前区间和所需要插入区间有交集
   <br>此时将当前区间和新区间合并，并更新新区建值用来和下一个区间进行比较
   
有个corner case需要注意的是，新区间可能在过完一遍当前集合之后仍然没有插入。所以此处维护一个boolean flag inserted。一来可以在确认新区间已经插入后直接将原有区间加入结果集；二来可以在用来解决上述corner case

#### Java代码实现

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        if (newInterval == null) {
            return intervals;
        }
        List<Interval> res = new ArrayList<>();
        boolean inserted = false; // the new interval is inserted and no further merge is required
        for (Interval interval : intervals) {
            if (inserted || interval.end < newInterval.start) {
                res.add(interval);
            } else if (interval.start > newInterval.end) {
                res.add(newInterval);
                inserted = true;
                res.add(interval);
            } else {
                newInterval.start = Math.min(interval.start, newInterval.start);
                newInterval.end = Math.max(interval.end, newInterval.end);
            }
        }
        if (!inserted) {
            res.add(newInterval);
        }
        return res;
    }
}

/*
    input types have been changed on April 15, 2019.
*/
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> res = new ArrayList<>();
        boolean inserted = false;
        
        for (int[] interval : intervals) {
            if (inserted || interval[1] < newInterval[0]) {
                res.add(interval);
            } else if (interval[0] > newInterval[1]) {
                res.add(newInterval);
                inserted = true;
                res.add(interval);
            } else {
                newInterval[0] = Math.min(newInterval[0], interval[0]);
                newInterval[1] = Math.max(newInterval[1], interval[1]);
            }
        }
        
        if (!inserted) {
            res.add(newInterval);
        }
        
        int[][] result = new int[res.size()][2];
        
        for (int i = 0; i < res.size(); i++) {
            result[i] = res.get(i);
        }
        return result;
        
    }
}



```