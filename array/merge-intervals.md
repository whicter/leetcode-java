# 56. Merge Intervals
### 题目描述

>Given a collection of intervals, merge all overlapping intervals.
<br>For example,
Given <span style="background-color:#ffe6e6"><font color=#cc0000 >[1, 3], [2, 6], [8, 10], [15, 18]</font></span>,
<br>return <span style="background-color:#ffe6e6"><font color=#cc0000 >[1, 6], [8, 10], [15, 18]</font></span>.

[原题链接](https://leetcode.com/problems/merge-intervals/description/)

### 解题思路
定义自己的comparator，重写Collections.sort

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
    public List<Interval> merge(List<Interval> intervals) {
        // In Java 8, it can be simplified to
        // intervals.sort((i1, i2) -> Integer.compare(i1.start, i2.start));
        Collections.sort(intervals, new Comparator<Interval>() {
            @Override
            public int compare(Interval i1, Interval i2) {
                return i1.start - i2.start;
            }
        });
        
        List<Interval> res = new ArrayList<>();
        Interval pre = null;
        for (Interval interval : intervals) {
            if (pre == null || interval.start > pre.end) {
                res.add(interval);
                pre = interval;
            } else if (interval.end > pre.end) {
                pre.end = interval.end;
            }
        }
        return res;
    }
}
```





