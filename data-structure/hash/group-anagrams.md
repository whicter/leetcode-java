# 49. Group Anagrams

### 题目描述

>Given an array of strings, group anagrams together.

#### Example:

    Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
    Output:
    [
      ["ate","eat","tea"],
      ["nat","tan"],
      ["bat"]
    ]
    
**Note:**

- All inputs will be in lowercase.
- The order of your output does not matter.

[原题链接](https://leetcode.com/problems/group-anagrams/)

### 解题思路
对每个单词的字符排序然后建立hash

####  Java代码实现

``` java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if (strs == null || strs.length == 0) {
            return new ArrayList<List<String>>();
        }
        
        Map<String, List<String>> anagramsMap = new HashMap<>();
        for (String str : strs) {
            char[] strArray = str.toCharArray();
            Arrays.sort(strArray);
            String key = String.valueOf(strArray);
            
            if (!anagramsMap.containsKey(key)) {
                anagramsMap.put(key, new ArrayList<String>(){{add(str);}});
            } else {
                anagramsMap.get(key).add(str);
            }
        }
        return new ArrayList<List<String>>(anagramsMap.values());
    }
}
```