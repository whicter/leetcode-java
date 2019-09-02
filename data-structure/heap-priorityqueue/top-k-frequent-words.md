# 692. Top K Frequent Words
### 题目描述
> Given a non-empty list of words, return the k most frequent elements.
>
> Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

#### Example 1:

Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.

#### Example 2:

Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
with the number of occurrence being 4, 3, 2 and 1 respectively.



[原题链接](https://leetcode.com/problems/top-k-frequent-words/)

### 解题思路
和[347. Top K Frequent Elements](data-structure/heap-priorityqueue/top-k-frequent-elements.md)一样的解法，只是需要注意的是要alphabetical order，在override comparator时候要多一个判断

#### Java代码实现
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> count = new HashMap();

        for (String word: words) {
            count.put(word, count.getOrDefault(word, 0) + 1);
        }

        PriorityQueue<String> heap = new PriorityQueue<String>((w1, w2) -> count.get(w1).equals(count.get(w2)) ? w2.compareTo(w1) : count.get(w1) - count.get(w2)); // enforcing alphabetical order

        for (String word: count.keySet()) {
            heap.offer(word);
            if (heap.size() > k) {
                heap.poll();
            }
        }

        List<String> ans = new ArrayList();
        while (!heap.isEmpty()) {
            ans.add(heap.poll());
        }

        Collections.reverse(ans);
        return ans;
    }
}
```