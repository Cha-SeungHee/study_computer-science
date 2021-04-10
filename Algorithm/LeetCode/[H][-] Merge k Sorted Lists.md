``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
import heapq


class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        head, cur = None, None
        
        heap = []
        
        for j in range(len(lists)):            
            if lists[j]:
                heapq.heappush(heap, (lists[j].val, j, lists[j]))
                
        while heap:
            val, j, node = heapq.heappop(heap)            
            
            if not head:
                head = ListNode(val)
                cur = head
            else:
                cur.next = ListNode(val)
                cur = cur.next
            if node.next:
                heapq.heappush(heap, (node.next.val, j, node.next))
        
        return head
```

j는 node의 val 값이 같을 때 다음으로 비교하기 위한 workaround  
j가 없으면 Node의 __lt__ 메소드를 찾으려고 하나 제공되는 ListNode 클래스는 해당 메소드를 구현하지 않음  
