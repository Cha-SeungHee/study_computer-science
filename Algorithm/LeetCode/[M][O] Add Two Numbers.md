``` py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        head = None
        cur = head
        
        carry = 0
        
        while l1 and l2:
            if not cur:
                head = ListNode((l1.val + l2.val) % 10)
                carry = (l1.val + l2.val) // 10
                cur = head
            else:
                cur.next = ListNode((l1.val + l2.val + carry) % 10)
                carry = (l1.val + l2.val + carry) // 10
                cur = cur.next            
            l1 = l1.next
            l2 = l2.next
        
        while l1:
            cur.next = ListNode((l1.val + carry) % 10)
            carry = (l1.val + carry) // 10
            cur = cur.next
            l1 = l1.next
        
        while l2:
            cur.next = ListNode((l2.val + carry) % 10)
            carry = (l2.val + carry) // 10
            cur = cur.next
            l2 = l2.next
        
        if carry > 0:
            cur.next = ListNode(carry)
        
        return head
```
