# 159. Longest Substring with At Most Two Distinct Characters

### 题目描述

> Given a string s , find the length of the longest substring t  that contains at most 2 distinct characters

#### Example 1
    Input: "eceba"
    Output: 3
    Explanation: t is "ece" which its length is 3.

#### Example 2
    Input: "ccaabbb"
    Output: 5
    Explanation: t is "aabbb" which its length is 5.    

[原题链接](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

### 解题思路

考虑维护一个移动窗口，需要一个start，一个end指针。这里有两个问题需要考虑：
- 出现第三个字符时候去掉哪个字符
<br>以**abac**为例，可以发现当扫描到**c**时，**a**是一定会被去掉的，但是如果去掉所有出现过的a，那么最后只剩下**c**了。这时应该是去掉所有出现的b，顺便去掉了最开始的**a**，从而得到**ac**。由此观之，选择标准应该是字符的最后出现的位置，最后出现的位置越左（早），则其出现被全部删除后所减小的长度越少。因此，应该删光最后出现位置在最左的字符。

- start 和 end 如何跳转

因此可以建立字典，用来记录字符出现的最后位置来决定需要删除的字符以及跳转位置

#### Java代码实现：

```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int len = s.length();
        if (len < 3) {
            return len;
        }
        
        int start = 0, end = 2, maxLen = 2;
        
        HashMap<Character, Integer> charMap = new HashMap<Character, Integer>();
        charMap.put(s.charAt(0), 0);
        charMap.put(s.charAt(1), 1);
        
        while (end < len) {
            char cur = s.charAt(end);
            charMap.put(cur, end);
            
            if (charMap.size() == 3) {
                int indexToRemove = Collections.min(charMap.values()); //删除最靠左的字符
                charMap.remove(s.charAt(indexToRemove));
                start = indexToRemove + 1;
            }
            
            maxLen = Math.max(maxLen, end - start + 1);
            end ++;
        }
        
        return maxLen;
    }
}   
```

一个更好的方法是用一个map来记录字符及其出现次数。右指针移动，不断更新map, 当发现map里的字符个数大于规定个数的时候，开始移动左指针，同时更新map,直到map里的字符个数等于规定个数，中间不断更新包含规定字符个数的最大长度。这样即使follow up扩展到k个字符也能适用

### Java代码实现
```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int left = 0;
        int i = 0;
        int maxLen = 0;
        while (i < s.length()) {
            
            // 根据右指针指的当前字符更新map
            char c = s.charAt(i);
            if (!map.containsKey(c)) {
                map.put(c, 1);
            } else {
                map.put(c, map.get(c) + 1);
            }
            
            // 移动左指针，直到map中字符数量降至规定数量
            while (map.size() > 2) {
                char leftChar = s.charAt(left);
                if (map.containsKey(leftChar)) {
                
                    // 注意会有重复元素，所以先减小次数，只有次数降至0，才删除元素
                    map.put(leftChar, map.get(leftChar) - 1);                     
                    if (map.get(leftChar) == 0) { 
                        map.remove(leftChar);
                    }
                }
                left++;
            }               
            maxLen = Math.max(maxLen, i - left + 1);
            i++;
        }
        return maxLen;
    }
}
```

最后附上一个纯线性不用hash map的方法
```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        // 这里的end是用来记录下一次start的跳转
        // end 只有在出现新字符时候回更新
        // start只有出现了和end不一样的字符时候才跳转
        
        int start = 0, end = -1;  
        int n = s.length();  
        int len = 0;  
        for (int i = 1; i < n; i++) {  
            if (s.charAt(i) == s.charAt(i - 1)) {
                continue;  
            }
            if (end >= 0 && s.charAt(i) != s.charAt(end)) {  
                len = Math.max(len, i - start);  
                start = end + 1;  
            }  
            end = i - 1;  
        }  
        return Math.max(len, n - start);  
    }
}
```

### 参考
- https://blog.csdn.net/whuwangyi/article/details/42451289 
- https://segmentfault.com/a/1190000004212721

