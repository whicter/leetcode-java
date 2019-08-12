# 244. Shortest Word Distance II

### 题目描述

> Design a class which receives a list of words in the constructor, and implements a method that takes two words word1 and word2 and return the shortest distance between these two words in the list. Your method will be called repeatedly many times with different parameters. 


#### Example

Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

    Input: word1 = “coding”, word2 = “practice”
    Output: 3
    
    Input: word1 = "makes", word2 = "coding"
    Output: 1

**Note:**
You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

[原题链接](https://leetcode.com/problems/shortest-word-distance-ii/)

### 解题思路

因为api会被反复调用，考虑将每个单词出现的位置用hash map记录一下

需要注意的是在找最小距离的时候，将位置较考前的pointer向后移动来找到新的最小值


#### Java代码实现

```java
class WordDistance {

    private Map<String, List<Integer>> wordLocationsMap = new HashMap<>();

    // Constructor
    public WordDistance(String[] words) {

        // Prepare a mapping from a word to all it's wordLocationsMap (indices).
        for (int i = 0; i < words.length; i++) {
            List<Integer> locations = this.wordLocationsMap.getOrDefault(words[i], new ArrayList<Integer>());
            locations.add(i);
            this.wordLocationsMap.put(words[i], locations);
        }
    }

    public int shortest(String word1, String word2) {
        List<Integer> loc1, loc2;

        // Location lists for both the words
        // the indices will be in SORTED order by default
        loc1 = this.wordLocationsMap.get(word1);
        loc2 = this.wordLocationsMap.get(word2);

        int l1 = 0, l2 = 0, minDiff = Integer.MAX_VALUE;
        
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