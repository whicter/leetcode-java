#76. Minimum Window Substring

### 题目描述

>Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

#### Example
>For example,
<br> S = <font color=red>“ADOBECODEBANC</font>
<br> T = <font color=red>“ADOBECODEABCBANC</font>
<br> Minimum window is "BANC"

[原题链接](https://leetcode.com/problems/minimum-window-substring/description/)

### 解题思路
建立一个字典，key是目标String的字符，value是计数，然后维护一个窗口。在移窗的时候可以跳过没在字典里面的字符（也就是这个串不需要包含且仅仅包含字典里面的字符，有一些不在字典的仍然可以满足要求），只要遇到没在字典里面的字符可以继续移动窗口右端，而移动窗口左端的条件是当找到满足条件的串之后，一直移动窗口左端直到有字典里的字符不再在窗口里。

在实现中就是维护一个HashMap，一开始key包含字典中所有字符，value就是该字符的数量，然后遇到字典中字符时就将对应字符的数量减一。算法的时间复杂度是O(n),其中n是字符串的长度，因为每个字符再维护窗口的过程中不会被访问多于两次。空间复杂度则是O(字典的大小)，也就是代码中T的长度。代码如下：

需要注意一些的细节是：
1. count只有在char的个数>= 0是才++， 因为有可能找到的新的字符属于字典，但是数量已经匹配完但是整个字符串尚未满足要求
<br>
2. 同理在逆向操作的时候只有个数 > 0时才count --

### Java代码实现

``` java
class Solution {
    public String minWindow(String s, String t) {
        if (s == null || s.length() == 0) {  
            return "";  
        }
        
        // Initialize the map with characters in string T
        Map<Character, Integer> map = new HashMap<>();  
        for (int i = 0; i < t.length(); i++)  {  
            if (map.containsKey(t.charAt(i))) {  
                map.put(t.charAt(i), map.get(t.charAt(i)) + 1);  
            } else {  
                map.put(t.charAt(i), 1);  
            }  
        }  
        int left = 0; // start of the window
        int count = 0; // count of the letters matched in map
        int minLen = s.length() + 1;
        int minStart = 0;
        
        for (int right = 0; right < s.length(); right ++) {
            char curChar = s.charAt(right);
            if (map.containsKey(curChar)) {
                map.put(curChar, map.get(curChar) - 1);  
                if (map.get(curChar) >= 0) {  
                    count ++;  
                }  
                while (count == t.length()) {
                    char leftChar = s.charAt(left);
                    if (right - left + 1 < minLen) {
                        minLen = right - left + 1;
                        minStart = left;
                    }
                    if (map.containsKey(leftChar)) {  
                        map.put(leftChar, map.get(leftChar) + 1);  
                        if (map.get(leftChar) > 0) {  
                            count--;  
                        }  
                    }
                    left ++;
                }
            }
        }
        
        String result;
        if (minLen > s.length()) {
            result = "";
        } else {
            result = s.substring(minStart, minStart + minLen);
        }
        return result;
    }
}
```