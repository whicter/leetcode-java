# 245. Shortest Word Distance III

### 题目描述

> Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

>word1 and word2 may be the same and they represent two individual words in the list.


#### Example

Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

Input: word1 = “makes”, word2 = “coding”
Output: 1

Input: word1 = "makes", word2 = "makes"
Output: 3

**Note:**
You may assume word1 and word2 are both in the list.

[原题链接](https://leetcode.com/problems/shortest-word-distance-iii/)

### 解题思路
思路和上一题差不多，需要注意的是将两个String相同的时候单独处理


#### Java代码实现

```java
class Solution {
    public int shortestWordDistance(String[] words, String word1, String word2) {
        Map<String, List<Integer>> wordLocationsMap = new HashMap<>();

        for (int i = 0; i < words.length; i++) {
            List<Integer> locations = wordLocationsMap.getOrDefault(words[i], new ArrayList<Integer>());
            locations.add(i);
            wordLocationsMap.put(words[i], locations);
        }


        // Location lists for both the words
        // the indices will be in SORTED order by default
        int minDiff = Integer.MAX_VALUE;

        List<Integer> loc1 = wordLocationsMap.get(word1);

        // process the case where two strings are the same
        if (word1.equals(word2)) {
            for (int i = 1; i < loc1.size(); i++) {
                minDiff = Math.min(minDiff, loc1.get(i) - loc1.get(i - 1));
            }
            return minDiff;
        }

        List<Integer> loc2 = wordLocationsMap.get(word2);

        int l1 = 0, l2 = 0;

        while (l1 < loc1.size() && l2 < loc2.size()) {
            minDiff = Math.min(minDiff, Math.abs(loc1.get(l1) - loc2.get(l2)));
            if (loc1.get(l1) < loc2.get(l2)) {
                l1++;
            } else {
                l2++;
            }
        }

        return minDiff;  
    }
}

/**
 * Your WordDistance object will be instantiated and called as such:
 * WordDistance obj = new WordDistance(words);
 * int param_1 = obj.shortest(word1,word2);
 */
```