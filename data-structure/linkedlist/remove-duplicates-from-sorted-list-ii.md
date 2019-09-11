# 82. Remove Duplicates from Sorted List II

### 题目描述

> Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.


#### Example 1
    Input: 1->2->3->3->4->4->5
    Output: 1->2->5

#### Example 2
    Input: 1->1->1->2->3
    Output: 2->3


[原题链接](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

### 解题思路
对于原子操作 f[i]:
1. 当node [i] 与 备选节点的值不同：
    a. 如果备选节点没有出现过：
        将备选节点放入列表
    b. 如果备选节点出现过
        当前节点作为新的备选节点
2.  当node [i] 与 备选节点的值相同：  
    将备选节点标记为已出现

因此需要维护的变量为：
1. 备选节点
2. 备选节点是否被访问过
3. 当前访问节点
4. 终选链表     
     
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
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        ListNode candidate = head;
        int candidateVal = candidate.val;
        boolean candidateAppeared = false;
        ListNode cur = head.next;
        
        while (cur != null) {
            if (cur.val != candidateVal) {
                if (candidateAppeared) {
                    candidateAppeared = false;
                    candidate = cur;
                    candidateVal = cur.val;
                    cur = cur.next;
                } else {
                    tail.next = candidate;
                    candidate = cur;
                    cur = cur.next;
                    candidateVal = candidate.val;
                    tail = tail.next;
                }
                
            } else {
                candidateAppeared = true;
                cur = cur.next;
            }
        }
        
        if (!candidateAppeared) {
            tail.next = candidate;
        } else {
            tail.next = null;
        }
        
        return dummy.next;
    }
}
```