# 92. Reverse Linked List II
### 题目描述
>Reverse a linked list from position m to n. Do it in one-pass.

#### Note: 1 ≤ m ≤ n ≤ length of list.

### Example
    Input: 1->2->3->4->5->NULL, m = 2, n = 4
    Output: 1->4->3->2->5->NULL


[原题链接](https://leetcode.com/problems/reverse-linked-list-ii/)

### 解题思路


### Java代码实现

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
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null) {
            return null;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode preNode = dummy;
        for (int i = 1; i < m; i++) {
            preNode = preNode.next;
        }
        
        ListNode currHead = preNode.next;
        
        //after reversing, the current node will become the tail;
        ListNode revTail = currHead;
        ListNode nextNode = currHead.next;
        
        for (int i = m; i < n; i++) {
            ListNode newNext = nextNode.next;
            
            // the previous nextNode becomes part of reverse
            nextNode.next = currHead;
            currHead = nextNode;
            nextNode = newNext;
        }
        preNode.next = currHead;
        revTail.next = nextNode;
        
        return dummy.next;
    }
}
```