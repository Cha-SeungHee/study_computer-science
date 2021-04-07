``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        count = 0
        
        result = []
        oddHead, oddCurrent = None, None
        evenHead, evenCurrent = None, None        
        
        while head is not None:            
            if count % 2 == 0:                
                if oddHead is None:
                    oddHead = head
                    oddCurrent = head
                else:
                    oddCurrent.next = head                    
                    oddCurrent = oddCurrent.next                
            else:                
                if evenHead is None:
                    evenHead = head
                    evenCurrent = head
                else:
                    evenCurrent.next = head
                    evenCurrent = evenCurrent.next   
            
            count += 1
            head = head.next
        
        if evenCurrent:
            evenCurrent.next = None
        
        if oddCurrent: 
            oddCurrent.next = evenHead
        
        while oddCurrent is not None:
            result.append(oddCurrent.val)
            oddCurrent = oddCurrent.next
        
        return oddHead
```
