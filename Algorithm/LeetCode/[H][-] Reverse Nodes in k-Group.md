``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        if k <= 1: 
            return head
        
        dummy = ListNode(0, head)
        prev = dummy
        
        while prev is not None:
            tail = prev
            
            count = 0            
            while tail and count < k:
                tail = tail.next
                count = count + 1

            if tail:    
                tail = self.reverseUnit(k, prev, tail.next)
            
            prev = tail
            
        return dummy.next
            
        
    def reverseUnit(self, k, before, after):
        stack = []
        current = before.next
        newBegin = newTail = newCurrent = None
        count = 0

        while count < k:
            stack.append(current)                
            current = current.next 
            count += 1

        while stack:                
            if newBegin is None:
                newBegin = stack.pop()
                newCurrent = newBegin
            else:
                newCurrent.next = stack.pop()
                newCurrent = newCurrent.next
                if newCurrent is not None:
                    newTail = newCurrent

        before.next = newBegin
        newTail.next = after
        
        return newTail
```
