# 4. Median of Two Sorted Arrays
### 题目描述

> There are two sorted arrays nums1 and nums2 of size m and n respectively.
Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

##### Example 1
> nums1 = [1, 3]
<br> nums2 = [2]
<br> The median is 2.0

##### Example 2:
>nums1 = [1, 2]
<br> nums2 = [3, 4]
<br> The median is (2 + 3)/2 = 2.5

[原题链接](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

### 解题思路
首先假设数组A和B的元素个数都大于k/2，我们比较A[k/2-1]和B[k/2-1]两个元素，这两个元素分别表示A的第k/2小的元素和B的第k/2小的元素。这两个元素比较共有三种情况：`>`、`<`和`=`。如果A[k/2-1] `<` B[k/2-1]，这表示A[0]到A[k/2-1]的元素都在A和B合并之后的前k小的元素中。换句话说，A[k/2-1]不可能大于两数组合并之后的第k小值，所以我们可以将其抛弃。

证明也很简单，可以采用反证法。假设A[k/2-1]大于合并之后的第k小值，我们不妨假定其为第（k+1）小值。由于A[k/2-1]小于B[k/2-1]，所以B[k/2-1]至少是第（k+2）小值。但实际上，在A中至多存在k/2-1个元素小于A[k/2-1]，B中也至多存在k/2-1个元素小于A[k/2-1]，所以小于A[k/2-1]的元素个数至多有k/2+ k/2-2，小于k，这与A[k/2-1]是第（k+1）的数矛盾。

当A[k/2-1]>B[k/2-1]时存在类似的结论。

当A[k/2-1]=B[k/2-1]时，我们已经找到了第k小的数，也即这个相等的元素，我们将其记为m。由于在A和B中分别有k/2-1个元素小于m，所以m即是第k小的数。(这里可能有人会有疑问，如果k为奇数，则m不是中位数。这里是进行了理想化考虑，在实际代码中略有不同，是先求k/2，然后利用k-k/2获得另一个数。)

通过上面的分析，我们即可以采用递归的方式实现寻找第k小的数。此外我们还需要考虑几个边界条件：

如果A或者B为空，则直接返回B[k-1]或者A[k-1]；
如果k为1，我们只需要返回A[0]和B[0]中的较小值；
如果A[k/2-1]=B[k/2-1]，返回其中一个；

--------------------- 
作者：yutianzuijin 
来源：CSDN 
原文：https://blog.csdn.net/yutianzuijin/article/details/11499917/ 

![](/assets/median_of_two_sorted_arrays.png)

###  Java代码实现

``` java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int total = nums1.length + nums2.length;
        if (total % 2 == 0) {
            return (findKth(total / 2 + 1, nums1, nums2, 0, 0) + findKth(total / 2, nums1, nums2, 0, 0)) / 2.0;
        } else {
            return findKth(total / 2 + 1, nums1, nums2, 0, 0);
        }
        
    }

     private int findKth(int k, int[] nums1, int[]nums2, int start1, int start2) {
        int len1 = nums1.length, len2 = nums2.length;
        
        if (start1 >= len1) {
            return nums2[start2 + k - 1];
        }
        
        if (start2 >= len2) {
            return nums1[start1 + k - 1];
        }
        
        if (k == 1) {
            return Math.min(nums1[start1], nums2[start2]);
        }
        
        int m1 = start1 + k / 2 - 1;
        int m2 = start2 + k / 2 - 1;
        
        int middle1 = m1 >= len1 ? Integer.MAX_VALUE : nums1[m1];
        int middle2 = m2 >= len2 ? Integer.MAX_VALUE : nums2[m2];
        
        if (middle1 < middle2) {
            return findKth(k - k / 2, nums1, nums2, start1 + k / 2, start2);
        } else {
            return findKth(k - k / 2, nums1, nums2, start1, start2 + k / 2);
        }
    }
}
```