``` py
from collections import deque


# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        queue = deque()
        mirror = []
        
        if root:
            queue.append(root)        
        
        while queue:
            size = len(queue)
            count = 0
            
            for _ in range(size):
                node = queue.popleft()
                count += 1
                if count == size:
                    mirror.append(node.val) 
                
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return mirror
```
