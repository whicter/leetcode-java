# 269. Alien Dictionary

### 题目描述

>There is a new alien language that uses the English alphabet. However, the order among the letters is unknown to you.
<br>You are given a list of strings words from the alien language's dictionary, where the strings in words are **sorted lexicographically** by the rules of this new language.
<br>Return a string of the unique letters in the new alien language sorted in **lexicographically increasing order** by the new language's rules. If there is no solution, return "". If there are multiple solutions, return any of them.
<br>A string s is **lexicographically smaller** than a string t if at the first letter where they differ, the letter in s comes before the letter in t in the alien language. If the first min(s.length, t.length) letters are the same, then s is smaller if and only if s.length < t.length.



#### Example 1:

    Input: words = ["wrt","wrf","er","ett","rftt"]
    Output: "wertf"

#### Example 2:

    Input: words = ["z","x"]
    Output: "zx"
    
#### Example 3:

    Input: words = ["z","x","z"]
    Output: ""
    Explanation: The order is invalid, so return "".

    

[原题链接](https://leetcode.com/problems/course-schedule-ii/)



### 解题思路
略

#### Java代码实现

``` java
public class Solution {
    /**
     * @param words: a list of words
     * @return: a string which is correct order
     */
    public String alienOrder(String[] words) {
        // Write your code here
        Map<Character, List<Character>> children = new HashMap<>();
        Map<Character, Integer> indegree = new HashMap<>();
        
        // Find all unique letters and initialize indree map
        for (String word : words) {
            for (char c : word.toCharArray()) {
                indegree.put(c, 0);
                children.put(c, new ArrayList<>());
            }
        }

        for (int i = 0; i < words.length - 1; i++) {
            String word1 = words[i];
            String word2 = words[i + 1];

            if (word1.length() > word2.length() && word1.startsWith(word2)) {
                return "";
            }

            for (int j = 0; j < Math.min(word1.length(), word2.length()); j++) {
                char c1 = word1.charAt(j); 
                char c2 = word2.charAt(j);
                if (c1 != c2) {
                    indegree.put(c2, indegree.get(c2) + 1);
                    List<Character> childrenC1 = children.get(c1);
                    childrenC1.add(c2);
                    children.put(c1, childrenC1);
                    break;
                }
            }
        }

        // as we should return the topo order with lexicographical order
        // we should use PriorityQueue instead of a FIFO Queue
        Queue<Character> queue = new PriorityQueue<>();
        StringBuilder result = new StringBuilder();

        
        for (Character c : indegree.keySet()) {
            if (indegree.get(c) == 0) {
                queue.offer(c);
            }
        }

        while (!queue.isEmpty()) {
            Character c = queue.poll();
            result.append(c);
            
            for (Character child : children.get(c)) {
                indegree.put(child, indegree.get(child) - 1);
                if (indegree.get(child) == 0) {
                    queue.offer(child);
                }
            }
        }

        if (result.length() < indegree.size()) {
            return "";
        }
        return result.toString();
    }

}
```