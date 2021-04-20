``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        dummy = ListNode(0, head)
        smallerDummy = ListNode(0)
        greaterDummy = ListNode(0)
        
        current = head
        smallerCurrent = smallerDummy
        greaterCurrent = greaterDummy        
        
        while current:            
            dummy.next = current.next
            current.next = None    
            
            if current.val < x:
                smallerCurrent.next = current
                smallerCurrent = smallerCurrent.next
            else:
                greaterCurrent.next = current
                greaterCurrent = greaterCurrent.next            
                
            current = dummy.next           
        
        smallerCurrent.next = greaterDummy.next
        
        return smallerDummy.next
```
