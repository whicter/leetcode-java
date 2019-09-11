# 445. Add Two Numbers II

### 题目描述

> You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
>
>You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

#### Example:

    Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
    Output: 7 -> 8 -> 0 -> 7

[原题链接](https://leetcode.com/problems/add-two-numbers-ii/)

### 解题思路
用Stack来存两个链表，然后逐个出栈计算结果
技巧在于构建链表来存放结果。每次更新完当前节点后，创造新节点指向当前节点。新节点用来存储进位以及下一次计算结果。然后把指针从当前节点指向新节点，这样就可以实现从后往前构建链表
     
#### Java代码实现

``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<Integer>();
        Stack<Integer> s2 = new Stack<Integer>();
        
        while (l1 != null) {
            s1.push(l1.val);
            l1 = l1.next;
        };
        while (l2 != null) {
            s2.push(l2.val);
            l2 = l2.next;
        }
        
        int sum = 0;
        ListNode list = new ListNode(0);
        
        while (!s1.empty() || !s2.empty()) {
            if (!s1.empty()) {
                sum += s1.pop();
            }
            if (!s2.empty()) {
                sum += s2.pop();
            }
            
            list.val = sum % 10;
            // Node for next digit or carry
            ListNode head = new ListNode(sum / 10);
            head.next = list;
            list = head;
            sum /= 10;
        }
        
        return list.val == 0 ? list.next : list;
    }
}
```