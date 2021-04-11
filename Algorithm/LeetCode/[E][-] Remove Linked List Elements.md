``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        preNode = ListNode(0, head)
        curNode = preNode
        nextNode = head
        
        while curNode:
            nextNode = curNode.next
            while nextNode:
                if nextNode.val == val:
                    nextNode = nextNode.next
                else:
                    break
            curNode.next = nextNode
            curNode = curNode.next
            
        return preNode.next
```
