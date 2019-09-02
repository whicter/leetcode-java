# 347. Top K Frequent Elements
### 题目描述
>Given a non-empty array of integers, return the k most frequent elements.

#### Example 1:

    Input: nums = [1,1,1,2,2,3], k = 2
    Output: [1,2]

#### Example 2:

    Input: nums = [1], k = 1
    Output: [1]

**Note:**
- You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
- Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
 



[原题链接](https://leetcode.com/problems/top-k-frequent-elements/solution/)

### 解题思路
hashmap记录frequency，然后用最小堆来维护
Java的优先队列是默认最小堆。这里需要最小堆的原因是因为每次超过k的时候需要把最小元素（堆顶）去掉

#### Java代码实现
```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        
        Map<Integer, Integer> frequencyMap = new HashMap<>();
        for (int num : nums) {
            int count = frequencyMap.getOrDefault(num, 0);
            frequencyMap.put(num, count + 1);
        }
        
        PriorityQueue<Map.Entry<Integer, Integer>> pq = new PriorityQueue<>((a, b) -> Integer.compare(a.getValue(), b.getValue()));
        
        for (Map.Entry<Integer, Integer> entry : frequencyMap.entrySet()) {
            pq.offer(entry);
            if (pq.size() > k) {
                pq.poll();
            }
        }
        
        List<Integer> res = new LinkedList<>();
        while (!pq.isEmpty()) {
            // res.add(0, pq.poll().getKey());
            // if the order needs to honor the frequencey from high to low 
            res.add(pq.poll().getKey()); 
        }
        return res;
        
        
    }
}
```