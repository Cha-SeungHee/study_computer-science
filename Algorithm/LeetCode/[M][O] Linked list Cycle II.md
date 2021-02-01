``` java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode walker1 = head;
        ListNode walker2 = head;
        ListNode runner = head;
        ListNode cycle = null;
        
        boolean overtake = false;
        
        while (runner != null && runner.next != null) {
            walker1 = walker1.next;
            runner = runner.next.next;
            
            if (walker1 == runner) {
                overtake = true;
                break;
            }
        }
        
        if (overtake) {
            while (walker1 != walker2) {
                walker1 = walker1.next;
                walker2 = walker2.next;
            }
            
            cycle = walker1;
        } else {
            cycle = null;
        }
        
        return cycle;
    }
}
```
