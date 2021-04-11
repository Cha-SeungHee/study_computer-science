``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy = ListNode(0, head)
        prevNode, curNode, nextNode = dummy, head, None
        newHead = None
        
        if curNode:
            nextNode = curNode.next
        
        while curNode and nextNode:               
            prevNode.next = nextNode  
            curNode.next = nextNode.next
            nextNode.next = curNode   
            
            prevNode = curNode                      
            curNode = curNode.next             
            if curNode:            
                nextNode = curNode.next
        
        return dummy.next        
```
