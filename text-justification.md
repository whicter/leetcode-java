# 68. Text Justification

### 题目描述

>Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.
<br>You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.
<br>Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.
<br>For the last line of text, it should be left justified and no extra space is inserted between words.

#### Example
<br> **words:** <span style="background-color:#ffcccc"><font color=#cc0000 >["This", "is", "an", "example", "of", "text", "justification."]</font></span>
<br> **L:** <span style="background-color:#ffcccc"><font color=#cc0000 >16</font></span>.
<br> Return the formatted lines as:
    [
       "This    is    an",
       "example  of text",
       "justification.  "
    ]

[原题链接](https://leetcode.com/problems/text-justification/description/)

### 解题思路
建立一个字典，key是目标String的字符，value是计数，然后维护一个窗口。在移窗的时候可以跳过没在字典里面的字符（也就是这个串不需要包含且仅仅包含字典里面的字符，有一些不在字典的仍然可以满足要求），只要遇到没在字典里面的字符可以继续移动窗口右端，而移动窗口左端的条件是当找到满足条件的串之后，一直移动窗口左端直到有字典里的字符不再在窗口里。

在实现中就是维护一个HashMap，一开始key包含字典中所有字符，value就是该字符的数量，然后遇到字典中字符时就将对应字符的数量减一。算法的时间复杂度是O(n),其中n是字符串的长度，因为每个字符再维护窗口的过程中不会被访问多于两次。空间复杂度则是O(字典的大小)，也就是代码中T的长度。代码如下： 

需要注意一些的细节是：
1. count只有在char的个数>= 0是才++， 因为有可能找到的新的字符属于字典，但是数量已经匹配完但是整个字符串尚未满足要求
<br> 
2. 同理在逆向操作的时候只有个数 > 0时才count --

###  Java代码实现

``` java
class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> res = new ArrayList<>();
        if (words == null || words.length == 0) {
            return res;  
        }
        
        int currentLetterCount = 0;
        int lastIndex = 0;
        
        for (int i = 0; i < words.length; i++) {
            if (currentLetterCount + words[i].length() + i - lastIndex > maxWidth) {
                int spaceNum = 0;
                int extraSpace = 0;
                if (i - lastIndex - 1 > 0) {
                    spaceNum = (maxWidth - currentLetterCount) / (i - lastIndex - 1);
                    extraSpace = (maxWidth - currentLetterCount) % (i - lastIndex - 1);
                }
                StringBuilder sb = new StringBuilder();
                for (int j = lastIndex; j < i; j++) {
                    sb.append(words[j]);
                    if (j < i - 1) {
                        for (int k = 0; k < spaceNum; k++) {  
                            sb.append(" ");  
                        }  
                        if (extraSpace > 0) {  
                            sb.append(" ");  
                        }  
                        extraSpace--;  
                    }
                }
                for (int j = sb.length(); j < maxWidth; j++) {  
                    sb.append(" ");  
                }         
                res.add(sb.toString());  
                currentLetterCount = 0;  
                lastIndex = i;  
            }
            currentLetterCount += words[i].length();  
        }
        
        StringBuilder sb = new StringBuilder();  
        for (int i = lastIndex; i < words.length; i++) {  
            sb.append(words[i]);  
            if (sb.length() < maxWidth) {
                sb.append(" ");  
            }
        }  
        for (int i = sb.length(); i < maxWidth; i++) {  
            sb.append(" ");  
        }  
        res.add(sb.toString());  
        return res;  
    }
}
```