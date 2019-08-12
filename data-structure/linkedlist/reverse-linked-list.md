# 206. Reverse Linked List
### 题目描述
> Reverse a singly linked list.

### Example
    Input: 1->2->3->4->5->NULL
    Output: 5->4->3->2->1->NULL


[原题链接](https://leetcode.com/problems/reverse-linked-list/)

### 解题思路
- Iterative: 见Section Summary
- Recursion: 
    <br>Tricky part在于如何找到子问题。本题中，子问题的推导是需要反向思维，即：假设站在当前节点看的时候，身后剩余的节点已经反转，而后将节点的下一节点返回来指向自己

#### Java代码实现
#### Iteration
``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
 
 /* Iteration */
class Solution {
    public ListNode reverseList(ListNode head) {
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode curr = head;
        ListNode prev = null;
        
        while (curr != null) {
            
            ListNode newCurr = curr.next;
            curr.next = prev;
            prev = curr;
            curr = newCurr;
            
        }
        return prev;
        
    }
}


```

#### Recursion
```java
/* Recursion */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode newHead = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
}
```