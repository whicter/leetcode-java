# 15. 3Sum

### 题目描述

>Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

#### Example

[原题链接](https://leetcode.com/problems/3sum/description/)

### 解题思路
基础简单题。需要考虑去重以及边界值

#### Java代码实现

``` java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) { 
        List<List<Integer>> res = new ArrayList<>();
        if (nums != null && nums.length >= 3) {
            Arrays.sort(nums);
            int len = nums.length;
            
            for (int i = 0; i < len; i++) {
                if (i > 0 && nums[i] == nums[i - 1]) {
                    continue;
                }    
                
                int cur = nums[i];
                int start = i + 1, end = len - 1;
                while (start < end) {
                    int startNum = nums[start];
                    int endNum = nums[end];
                    
                    if (startNum + endNum + cur == 0) {
                        res.add(
                            new ArrayList<Integer>(){{
                                add(cur);
                                add(startNum);
                                add(endNum);
                            }}
                        );
                        
                        while (start + 1 < len && nums[start + 1] == startNum) {
                            start ++;
                        }
                        while (end - 1 >= 0 && nums[end - 1] == endNum) {
                            end --;
                        }
                        
                        start ++;
                        end --;
                    } else if (startNum + endNum + cur < 0) {
                        start ++;
                    } else {
                        end --;
                    }
                
                }
            }
        }
        return res;
        
    }
}
```