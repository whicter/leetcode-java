# 19. Remove Nth Node From End of List

### 题目描述

> Given a linked list, remove the nth node from the end of list and return its head.


#### Example
> Given linked list: 1->2->3->4->5, and n = 2.
<br> After removing the second node from the end, the linked list becomes 1->2->3->5.


[原题链接](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

### 解题思路
只需要遍历列表一次即可。 保持快指针领先n + 1个身位。当快指针已经指向空的时候，慢指针刚好在目标节点前一个位置

题设里n永远都是小于链表长度的，答案里我加了判断，如果n是大于链表长度，最后的结果是返回原链表

####  Java代码实现

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return head;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode slow = dummy;
        ListNode fast = dummy;

        for (int i = 0; i <= n; i++) {
            fast = fast.next;
            if (fast == null) {
                break;
            }
        }

        while (fast != null) {
            slow = slow.next;
            fast = fast.next;
        }

        slow.next = slow.next.next;
        return dummy.next;
    }
}
```