# 23. Merge K Sorted Lists
### 题目描述

> Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

[原题链接](https://leetcode.com/problems/merge-k-sorted-lists/description/)

### 解题思路
使用Priority Queue。这样保持每次取出的节点中是当前最小的，依次加入新的链表，从而得到合并的结果。
这个算法每个元素要读取一次，即是k*n次，然后每次读取元素要把新元素插入堆中要logk的复杂度，所以总时间复杂度是O(nklogk)。空间复杂度是堆的大小，即为O(k)。
###  Java代码实现

``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        // new PriorityQueue<>(lists.length, Comparator.comparingInt(o -> o.val));
        PriorityQueue<ListNode> pq = new PriorityQueue<>(lists.length, (o1, o2) -> {
            return Integer.compare(o1.val, o2.val);
        });
        
        ListNode dummy = new ListNode(0);
        ListNode walk = dummy;
        
        for (ListNode node : lists) {
            if (node != null) {
                pq.offer(node);
            }
        }
        
        while (!pq.isEmpty()) {
            walk.next = pq.poll();
            walk = walk.next;
        
        
            if (walk.next != null) {
                pq.add(walk.next);       
            }
        }
        return dummy.next;
    }
}
```