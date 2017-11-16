### 题目描述

>Given a string, sort it in decreasing order based on the frequency of characters.

##### Example 1
>**Input:**
"tree"
**Output:**
"eert"
**Explanation:**
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.

##### Example 2:
>**Input:**
"cccaaa"
**Output:**
"cccaaa"
**Explanation:**
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.

##### Example 3:
>**Input:**
"Aabb"
**Output:**
"bbAa"
**Explanation:**
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.

[原题链接](https://leetcode.com/problems/sort-characters-by-frequency/description/)


### 解题思路

非常容易的一道题，trick在于buildArray，找到max count以后建立一个以此为size的array然后把放入对应的字母
###  Java代码实现

``` java
class Solution {
    public String frequencySort(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }
        int maxCount = 0;
        Map<Character, Integer> charFreqMap = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            Integer charCount = charFreqMap.get(c);
            if (charCount == null) {
                charCount = 0;
            }
            
            charCount ++;
            charFreqMap.put(c, charCount);
            maxCount = Math.max(maxCount, charCount);
        }
        List<Character>[] array = buildArray(charFreqMap, maxCount);

        return buildString(array);
    }
    
    private List<Character>[] buildArray(Map<Character, Integer> map, int maxCount) {
        List<Character>[] array = new List[maxCount + 1];
        for (Character c : map.keySet()) {
            int count = map.get(c);
            if (array[count] == null) {
                array[count] = new ArrayList();
            }
            array[count].add(c);
        }
        return array;
    }

    private String buildString(List<Character>[] array) {
        StringBuilder sb = new StringBuilder();
        for (int i = array.length - 1; i > 0; i--) {
            List<Character> list = array[i];
            if (list != null) {
                for (Character c : list) {
                    for (int j = 0; j < i; j++) {
                        sb.append(c);
                    }
                }
            }
        }
        return sb.toString();
    }
}
```