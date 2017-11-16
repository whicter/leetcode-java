# Word Ladder
### 题目描述

>Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:
>- Only one letter can be changed at a time.
>- Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

##### Example
>Given:
beginWord = <span style="background-color:#ffe6e6"><font color=#cc0000 >"hit"</font></span>
<br>endWord = <span style="background-color:#ffe6e6"><font color=#cc0000 >"cog"</font></span>
wordList = <span style="background-color:#ffe6e6"><font color=#cc0000 >["hot","dot","dog","lot","log","cog"]</font></span>
As one shortest transformation is <span style="background-color:#ffe6e6"><font color=#cc0000 >"hit" -> "hot" -> "dot" -> "dog" -> "cog"</font></span>,
return its length <span style="background-color:#ffe6e6"><font color=#cc0000 >5</font></span>.

##### Note:
>- Return 0 if there is no such transformation sequence.
>- All words have the same length.
>- All words contain only lowercase alphabetic characters.
>- You may assume no duplicates in the word list.
>- You may assume beginWord and endWord are non-empty and are not the same.

[原题链接](https://leetcode.com/problems/word-ladder/description/)

### 解题思路

 经典的BFS题目。
 想象一下，这个变换过程是一个树，
 每一层是当前所有的变换结果 ，
 下一层又是上一层的字符串的所有的变换结果。
 
例子：HIT
 AIT, BIT, CIT, DIT.....     
 HAT, HBT, HCT, HDT.....    
 HIA, HIB, HIC, HID....
 HIT 可以有这么多种变换方式，
 而AIT, BIT本身也可以以相同的方式展开，
 这就形成了一个相当大的树。
  
 最直观的思路就是DFS，每次变成字典中的某个新单词，
 同时从字典中删除这个单词然后不断递归。
 但是大数据时候超时。因为要求的是最短的变换次数，
 所以可以使用BFS，和DFS不一样不一次走到最深。
 逐层遍历变换了一次、二次、三次、n次的所有单词。
  
 思考一下DFS和BFS的区别，举个最简单的例子，111 -> 311。
 DFS的话，111->112，之后需要DFS 112的所有变形。
 同理111->113之后还要遍历113的所有变形。
 而BFS的话，
    111
                               112  113 121 131  211  311
 只需要6次就能找到最终结果。


![word ladder.jpg](http://upload-images.jianshu.io/upload_images/318609-19d340952ed87d09.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


###  Java代码实现

``` java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> words = new HashSet(wordList);
        
        if (beginWord == null || endWord == null 
         || beginWord.length() == 0 || endWord.length() == 0
         || beginWord.length() != endWord.length() || !words.contains(endWord)) {
             return 0 ;
         }
        
        Queue <String> q = new LinkedList<>();
        q.offer(beginWord);
        
        Set<String> visited = new HashSet<>();
        visited.add(beginWord);
        
        int level = 0;
        
        while (!q.isEmpty()) {
            int qSize = q.size();
            level++;
            
            for (int i = 0; i < qSize; i++) {
                String current = q.poll();
                for (int j = 0; j < current.length(); j++) {
                    char[] stringChar = current.toCharArray();
        
                    for (char c = 'a'; c <= 'z'; c++) {
                        stringChar[j] = c;

                        String temp = new String(stringChar);
                        
                        if (endWord.equals(temp)) {
                            return level + 1;
                        }
                        
                        if (words.contains(temp) && !visited.contains(temp)) {
                            visited.add(temp);
                            q.offer(temp);
                        }
                    }
                }
            }
        }
        return 0;
        
    }
}
```