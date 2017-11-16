# 25. Reverse Nodes in k-Group
### 题目描述

> Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.
<br> k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.
<br> You may not alter the values in the nodes, only nodes itself may be changed.
<br> Only constant memory is allowed.

##### Example
> Given this linked list: 1->2->3->4->5
<br> For k = 2, you should return: 2->1->4->3->5
<br> For k = 3, you should return: 3->2->1->4->5


[原题链接](https://leetcode.com/problems/reverse-nodes-in-k-group/description//)

### 解题思路
每k个一组翻转列表，核心在于reverse method， 具体看图解
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
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || k == 1) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        
        int looper = 0;
        ListNode traverse = head;
        
        while (traverse != null) {
            looper ++;
            if (looper % k == 0) {
                pre = reverse(pre, traverse.next);
                traverse = pre.next;
            } else {
                traverse = traverse.next;
            }
        }
        return dummy.next;
        
    }
    /*
     * 0->1->2->3->4->5->6
     * |           |   
     * pre        next
     *
     * after calling pre = reverse(pre, next)
     * 
     * 0->3->2->1->4->5->6
     *          |  |
     *          pre next 
     */
    public ListNode reverse(ListNode pre, ListNode next) {
        ListNode last = pre.next;
        ListNode curr = last.next;
        
        while (curr != next) {
            last.next = curr.next;
            curr.next = pre.next;
            pre.next = curr;
            curr = last.next;
        }
        return last;    
    }
}
```