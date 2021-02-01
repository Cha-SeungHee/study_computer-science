```java  
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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) return null;
        
        ListNode slow = null;
        ListNode fast = null;
        int count = n+1;
        
        while (count > 0) {
            if (fast == null) {
                fast = head;
            } else {
                fast = fast.next;
            }
            count = count-1;
            if (fast == null) break;
        }
        
        if (fast == null && count > 1) return null;
        
        while (fast != null) {
            if (slow == null) {
                slow = head;
            } else {
                slow = slow.next;    
            }            
            fast = fast.next;
        }        
        
        if (slow == null) {
            head = head.next;
        } else {
            slow.next = slow.next.next;    
        }
        
        return head;
    }
}
```
