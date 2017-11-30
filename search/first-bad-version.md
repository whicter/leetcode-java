# 34. Search for a Range
### 题目描述

> You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.
<br> Suppose you have <span style="background-color:#ffe6e6"><font color=#cc0000>
n</font></span> versions <span style="background-color:#ffe6e6"><font color=#cc0000>
[1, 2, ..., n]</font></span> and you want to find out the first bad one, which causes all the following ones to be bad.
<br>You are given an API <span style="background-color:#ffe6e6"><font color=#cc0000>
bool isBadVersion(version)</font></span> which will return whether <span style="background-color:#ffe6e6"><font color=#cc0000>
version</font></span> is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.


[原题链接](https://leetcode.com/problems/first-bad-version/description/)

### 解题思路
Binary Search的变体，需要找到最左边的目标。


###  Java代码实现

``` java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int start = 1, end = n, res = -1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (isBadVersion(mid)) {
                res = mid;
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        return res;
    }
}
```