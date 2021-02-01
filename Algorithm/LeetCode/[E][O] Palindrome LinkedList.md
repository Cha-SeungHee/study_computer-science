``` java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null) return true;
        
        ListNode runner = head;
        ListNode walker = head;
        Stack<Integer> stack = new Stack<>();
        
        while (runner != null && runner.next != null) {
            stack.push(walker.val);
            runner = runner.next.next;
            walker = walker.next;            
        }
        
        if (runner != null) {
            walker = walker.next;
        }
        
        while (!stack.isEmpty()) {
            int num = stack.pop();

            if (num != walker.val) return false;
            
            walker = walker.next;
        }
        
        return true;
    }
}
```
