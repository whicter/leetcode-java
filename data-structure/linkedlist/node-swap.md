## Reverse list
```java
/*
    Starting status: prev = null
                     0->1->2->3->4->5->6
                     |
                    curr
    
    1st iteration:   1->null
                     |
                    prev
    
                     2->3->4->5->6
                     |
                    curr
    
    2nd iteration:   2->1->null
                     |
                    prev
    
                     3->4->5->6
                     |
                    curr
*/
while (curr != null) {
    
    ListNode newCurr = curr.next;
    curr.next = prev;
    prev = curr;
    curr = newCurr;
    
}

```

## Reverse partial of the list given the pre node and the next node
``` java
/*

   0->1->2->3->4->5->6
   |  |           |   
 pre  last        next
     
   1 is last since after reversing, it will be the last one of the partial list  
   
   after calling pre = reverse(pre, next)
   
   0->4->3->2->1->5->6
   |            |  |
  pre        last  next 
  

reverse 1->2->3->4 to 2->1->3->4 to 3->2->1->4 to 4->3->2->1  

*/  

ListNode last = pre.next;
ListNode curr = last.next;

while (curr != next) {
    // 0->1->3->4  2->3
    last.next = curr.next;
    
    // 2->1->3->4  0->1
    curr.next = pre.next;
    
    // 0->2->1->3->4
    pre.next = curr;
    
    // curr = 3
    curr = last.next;
}

// return pre.next if head is required
return last;    
```

## Simplified version of the previous case of reversing the entire list

``` java
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

```
