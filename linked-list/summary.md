## Reverse partial of the list given the pre node and the next node
``` java
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
// reverse 1->2->3 to 3->2->1    

public ListNode reverse(ListNode pre, ListNode next) {
    ListNode last = pre.next;
    ListNode curr = last.next;
    
    while (curr != next) {
        last.next = curr.next;
        curr.next = pre.next;
        pre.next = curr;
        curr = last.next;
    }
    
    // return pre.next if head is required
    return last;    
}
```

## Simplified version of the previous case of reversing the entire list

``` java
public ListNode reverse(ListNode head) {
    // assume head is not null
    ListNode dummy = new ListNode(0);
    dummy.next = head;

    ListNode walk = head;
    ListNode curr = walk.next;
    
    while (curr != null) {
        walk.next = curr.next;
        curr.next = dummy.next;
        dummy.next = curr;
        curr = walk.next;
    }
    return dummy.next; 
}   
```
