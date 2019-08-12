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
From [Code Ganker](http://blog.csdn.net/linhuanmars/article/details/24063271)
这道题属于纯粹的字符串操作，要把一串单词安排成多行限定长度的字符串。主要难点在于空格的安排。
- 首先每个单词之间必须有空格隔开，而当当前行放不下更多的单词并且字符又不能填满长度L时，我们要把空格均匀的填充在单词之间。
- 如果剩余的空格量刚好是间隔倍数那么就均匀分配即可，否则还必须把多的一个空格放到前面的间隔里面。

实现中我们维护一个count计数记录当前长度，超过之后我们计算共同的空格量以及多出一个的空格量，然后将当行字符串构造出来。

最后一个细节就是最后一行不需要均匀分配空格，句尾留空就可以，所以要单独处理一下。

时间上我们需要扫描单词一遍，然后在找到行尾的时候在扫描一遍当前行的单词，不过总体每个单词不会被访问超过两遍，所以总体时间复杂度是O(n)。而空间复杂度则是结果的大小（跟单词数量和长度有关，不能准确定义，如果知道最后行数r，则是O(r*L)）。代码如下： 

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