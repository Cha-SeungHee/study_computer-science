``` java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;
        
        int lengthA = 0, lengthB = 0;
        ListNode walkerA = headA;
        ListNode walkerB = headB;
        
        while (walkerA != null) {
            lengthA = lengthA + 1;
            
            walkerA = walkerA.next;
        }
        
        while (walkerB != null) {
            lengthB = lengthB + 1;
            
            walkerB = walkerB.next;
        }
        
        while (lengthA > lengthB) {
            headA = headA.next;
            
            lengthA = lengthA - 1;
        }
        
        while (lengthB > lengthA) {
            headB = headB.next;
            
            lengthB = lengthB - 1;
        }
        
        while (headA != null && headB != null && headA != headB) {
            headA = headA.next;
            headB = headB.next;
        }
        
        if (headA == null || headB == null) return null;
        
        return headA;
    }
}
```
