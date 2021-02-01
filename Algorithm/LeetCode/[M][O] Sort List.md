``` java
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null) return null;
        
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        ListNode walker = head;
        while (walker != null) {
            pq.offer(walker.val);
            
            walker = walker.next;
        }
        
        walker = head;
        while (!pq.isEmpty()) {
            walker.val = pq.poll();
            
            walker = walker.next;
        }
            
        return head;
    }
}
```

- mergeSort / constant memory로 풀어보기  
