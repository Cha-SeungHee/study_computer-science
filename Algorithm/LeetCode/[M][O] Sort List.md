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


``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        
        begin = head
        mid = self.getMid(begin)
        tail = mid.next
        mid.next = None
        
        sortedBegin = self.sortList(begin)
        sortedTail = self.sortList(tail)
        return self.mergeList(sortedBegin, sortedTail)    
    
    
    def getMid(self, node):
        walker, runner = node, node.next
        
        while runner and runner.next:
            walker = walker.next
            runner = runner.next.next
        
        return walker
    
    
    def mergeList(self, begin, tail):
        current = dummy = ListNode()
        
        while begin and tail:
            if begin.val < tail.val:
                current.next = begin
                begin = begin.next
            else:
                current.next = tail
                tail = tail.next
            current = current.next
        
        while begin:
            current.next = begin
            begin = begin.next
            current = current.next
        
        while tail:
            current.next = tail
            tail = tail.next
            current = current.next
        
        return dummy.next
```
