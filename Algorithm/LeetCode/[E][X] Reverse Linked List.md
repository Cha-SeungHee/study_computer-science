``` java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode reverseHead = null;
        
        while (head != null) {
            ListNode node = new ListNode(head.val);
            
            if (reverseHead == null) {
                reverseHead = node;
            } else {
                node.next = reverseHead;
                reverseHead = node;
            }
            
            head = head.next;
        }
        
        return reverseHead;
    }
}
```
