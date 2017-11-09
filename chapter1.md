#242. Valid Anagram

### 题目描述

>Given two strings *s* and *t*, write a function to determine if *t* is an anagram of *s*.
For example,*s* = "anagram", *t* = "nagaram", return true.*s* = "rat", *t* = "car", return false.

>**Note:** You may assume the string contains only lowercase alphabets.
**Follow up:** What if the inputs contain unicode characters? How would you adapt your solution to such case? 

[原题链接](https://leetcode.com/problems/valid-anagram/)

### 解题思路
用一个长度为26的int array来模拟hashmap
类似题目还有[Ransom Note](https://leetcode.com/problems/ransom-note/)
###  Java代码实现

``` java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s == null || t == null || s.length() != t.length()) {
            return false;
        }
        
        int[] arr = new int[26];
        int len = s.length();
        for (int i = 0; i < len; i++) {
            arr[s.charAt(i) - 'a'] ++;
        }
        
        for (int i = 0; i < len; i++) {
            if (--arr[t.charAt(i) - 'a'] < 0) {
                return false;
            }
        }
        
        return true;
    }
}
```