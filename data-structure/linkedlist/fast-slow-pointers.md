## Node Definition
``` java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
```
## Find Middle Node
``` java
public ListNode findMiddle(ListNode head) {
    ListNode fast = head;
    ListNode slow = head.next;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```

## Find kth Node from back
This is usually be done by keeping fast and slow nodes with a distance of n

## Linked List Has Cycle

``` java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }
        
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast && slow != null) {
                return true;
            }
        }
        return false;
    }
}
```