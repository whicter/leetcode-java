# 852. Peak Index in a Mountain Array
### 题目描述

> Let's call an array A a mountain if the following properties hold:
>- A.length >= 3
>- There exists some 0 < i < A.length - 1 such that A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1] 
> Given an array that is definitely a mountain, return any i such that A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1].

### Example 1:

    Input: [0,1,0]
    Output: 1

### Example 2:

    Input: [0,2,1,0]
    Output: 1

[原题链接](https://leetcode.com/problems/peak-index-in-a-mountain-array/)



### 解题思路
如果中间部分有重复数字，那只能线性遍历。


### Java代码实现

``` java
class Solution {
    public int peakIndexInMountainArray(int[] A) {
        int start = 0, end = A.length - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (A[mid] < A[mid + 1])
                start = mid + 1;
            else
                end = mid - 1;
        }
        return start;
    }
}
```