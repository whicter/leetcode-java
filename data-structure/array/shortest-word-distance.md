# 243. Shortest Word Distance

### 题目描述

> Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.


#### Example
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

    Input: word1 = “coding”, word2 = “practice”
    Output: 3

    Input: word1 = "makes", word2 = "coding"
    Output: 1
**Note:**
You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

[原题链接](https://leetcode.com/problems/shortest-word-distance/)

### 解题思路

Easy级别题，没什么好说的...可以设置一个indexUpdated的flag来判断在有重复String的时候index是否有更新

可以看一下更有意思的相关题：
- [244. Shortest Word Distance II](/data-structure/hash/shortest-word-distance-ii.md)
- [245. Shortest Word Distance III](/data-structure/hash/shortest-word-distance-iii.md)


#### Java代码实现

```java
class Solution {
    public int shortestDistance(String[] words, String word1, String word2) {
    int i1 = -1;
    int i2 = -1;
        
    int minDistance = Integer.MAX_VALUE;
    
    boolean indexUpdated = false;    
    for (int i = 0; i < words.length; i++) {
        if (words[i].equals(word1)) {
            i1 = i;
            indexUpdated = true;
            
        } else if (words[i].equals(word2)) {
            i2 = i;
        }

        if (i1 != -1 && i2 != -1 && indexUpdated) {
            minDistance = Math.min(minDistance, Math.abs(i1 - i2));
        }
    }
    return minDistance;
}


```