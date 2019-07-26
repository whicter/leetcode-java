# 1048. Longest String Chain

### 题目描述

>Given a list of words, each word consists of English lowercase letters.
<br>Let's say word1 is a predecessor of word2 if and only if we can add exactly one letter anywhere in word1 to make it equal to word2.  For example, "abc" is a predecessor of "abac".
<br>A word chain is a sequence of words [word_1, word_2, ..., word_k] with k >= 1, where word_1 is a predecessor of word_2, word_2 is a predecessor of word_3, and so on.
<br>Return the longest possible length of a word chain with words chosen from the given list of words.

### Example:

    Input: ["a", "b", "ba", "bca", "bda", "bdca"]
    Output: 4
    Explanation: one of the longest word chain is "a","ba","bda","bdca".



[原题链接](https://leetcode.com/problems/word-search/)

### 解题思路
原子操作f(k): longest chain end with words[k]
f(k) = max{ h(k, k - i) && g(k - i) + 1}
h(k, k - i): 判断works[k]去掉charAt(i)后是否存在于words
g(k - i): longest chain end end with word[k] without charAt(i)

需要维护的变量：
maxChainLength
Map with key: word, value: length

### Java代码实现：

```java
class Solution {
    public int longestStrChain(String[] words) {
        Arrays.sort(words, (a,b) -> a.length() - b.length());
        
        HashMap<String, Integer> chainLengthMap = new HashMap<String, Integer>();
        int longestChain = Integer.MIN_VALUE;

        for (String word : words) {
            /* 
            if (chainLengthMap.containsKey(word)) {
                continue;
            }
            */
            chainLengthMap.put(word, 1);
            for (int i = 0; i < word.length(); i++) {
                StringBuilder sb = new StringBuilder(word);
                sb.deleteCharAt(i);
                String after = sb.toString();
                if (chainLengthMap.containsKey(after)) {
                    int chainLengthForPred = chainLengthMap.get(after);
                    if (chainLengthForPred+ 1 > chainLengthMap.get(word)) {
                        // update length for current word
                        chainLengthMap.put(word, chainLengthMap.get(after) + 1);
                    }
                }
            }
            if (chainLengthMap.get(word) > longestChain) {
                longestChain = chainLengthMap.get(word);
            }
        }
        return longestChain;
    }
    
    
}
```

