``` py
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""

class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        map = {}
        
        def clone(node):
            if node is None:
                return None
            
            if node in map:
                return map[node]
        
            newNode = Node(node.val)
            for neigh in node.neighbors:
                map[node] = newNode
                newNode.neighbors.append(clone(neigh))
                
            return newNode
    
        return clone(node)
```
