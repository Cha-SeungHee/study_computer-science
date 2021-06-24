``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        
        int carry = 0;
        ListNode dummy = new ListNode(0);        
        ListNode current = dummy;
        
        while (carry > 0 || l1 != null || l2 != null)  {
            int sum = carry;
            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }
            
            int digit = sum % 10;
            carry = sum / 10;
            
            current.next = new ListNode(digit);
            current = current.next;
        }
        
        return dummy.next;
    }
}
```

``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1:
            return l2
        
        if not l2:
            return l1
        
        dummy = ListNode(0)
        cur = dummy
        carry = 0
        
        while (carry > 0 or l1 or l2):
            num = carry

            if l1 is not None:
                num += l1.val
                l1 = l1.next
            if l2 is not None:
                num += l2.val
                l2 = l2.next
                
            digit = num % 10
            carry = num // 10
            
            cur.next = ListNode(digit)
            cur = cur.next
            
        return dummy.next
```
