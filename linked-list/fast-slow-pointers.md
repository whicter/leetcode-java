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


