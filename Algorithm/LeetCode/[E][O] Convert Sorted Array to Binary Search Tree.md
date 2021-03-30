``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:        
        return self.binaryTree(nums, 0, len(nums)-1)    
    
    def binaryTree(self, nums: List[int], begin: int, end: int) -> TreeNode:
        if begin > end:
             return None
    
        mid = begin + (end-begin)//2
        node = TreeNode(nums[mid])
        node.left = self.binaryTree(nums, begin, mid-1)
        node.right = self.binaryTree(nums, mid+1, end)
        
        return node
```
