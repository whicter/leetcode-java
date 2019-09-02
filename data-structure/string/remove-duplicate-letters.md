# 316. Remove Duplicate Letters

### 题目描述

>Given a string which contains only lowercase letters, remove duplicate letters so that every letter appears once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

#### Example 1:

    Input: "bcabc"
    Output: "abc"

#### Example 2:

    Input: "cbacdcbc"
    Output: "acdb"

[原题链接](https://leetcode.com/problems/remove-duplicate-letters/)

### 解题思路
首先我们需要明确题意`lexicographical order`。任何以`a`为起始的单词都要比非`a`起始的要更前。这也是为什么**Example 2**中的结果是`acdb`而不是`adbc`

在遍历每个字符的时候，我们用栈来维护结果集：
- 如果当前元素 < 栈顶元素且栈顶元素的位置不是最后位置，执行pop后将当前元素放入stack
- 如果当前元素已经在结果集中，直接跳过

因此我们还需要：
一个hashmap来记录每个字母出现的最后位置。
一个hashset来记录已经有的字母



#### Java代码实现

``` java
class Solution {
    public String removeDuplicateLetters(String s) {

        Stack<Character> stack = new Stack<>();

        // Keep track of the letters in the final result
        Set<Character> resultsSet = new HashSet<>();

        // this will let us know if there are any more instances of s[i] left in s
        Map<Character, Integer> lastPositionMap = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            lastPositionMap.put(s.charAt(i), i);
        }

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            // we can only try to add c if it's not already in our solution
            // this is to maintain only one of each character
            if (!resultsSet.contains(c)) {
                // if the last letter in our solution:
                //     1. exists
                //     2. is greater than c(so removing it will make the string smaller)
                //     3. it's not the last occurrence
                // we remove it from the solution to keep the solution optimal
                while (!stack.isEmpty() 
                       && c < stack.peek() 
                       && lastPositionMap.get(stack.peek()) > i) {
                    resultsSet.remove(stack.pop());
                }
                resultsSet.add(c);
                stack.push(c);
            }
        }
        StringBuilder sb = new StringBuilder(stack.size());
        for (char c : stack) {
            sb.append(c);
        }
        return sb.toString();
    }
}
```