``` py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        first = True
        prev = 0
        
        def inorder(node):
            nonlocal first, prev
            
            if node is None:
                return True
            
            left = inorder(node.left)
            
            if not left:
                return False
            
            if first:                
                first = False
            else:
                if node.val <= prev:
                    return False                
            prev = node.val
            
            return inorder(node.right)
        
        
        return inorder(root)
```
