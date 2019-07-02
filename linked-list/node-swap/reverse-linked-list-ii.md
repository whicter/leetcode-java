# 92. Reverse Linked List II
### 题目描述
>Reverse a linked list from position m to n. Do it in one-pass.

#### Note: 1 ≤ m ≤ n ≤ length of list.

### Example
    Input: 1->2->3->4->5->NULL, m = 2, n = 4
    Output: 1->4->3->2->5->NULL


[原题链接](https://leetcode.com/problems/reverse-linked-list-ii/)

### 解题思路
和Summary里的反转partial list差不多，只是在这里并没有给出终止节点，只给出计数，所以用for循环来找到终止点

反转的思路大致一样，一个个换位置。
因为是反转部分列表，所以我们需要知道的信息有：
- pre
- new head
- new tail
- next

鉴于next节点没有直接给出，因此需要我们动态维护的变量就是new head和next
pre和new tail都是固定的，new tail即pre.next


### Java代码实现

``` java
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
        
        // find the previous node of the partial list head
        ListNode preNode = dummy;
        for (int i = 1; i < m; i++) {
            preNode = preNode.next;
        }
        
        ListNode currHead = preNode.next;

        //after reversing, the current node will become the tail;
        ListNode last = currHead;

        // nextNode would be the next node of the last node in the partial list
        ListNode nextNode = currHead.next;
        
        for (int i = m; i < n; i++) {
            ListNode newNext = nextNode.next;
            // the previous nextNode becomes part of reverse
            nextNode.next = currHead;
            currHead = nextNode;
            nextNode = newNext;
        }

        // connect the partial list 
        preNode.next = currHead;
        last.next = nextNode;
        
        return dummy.next;
    }
}

```