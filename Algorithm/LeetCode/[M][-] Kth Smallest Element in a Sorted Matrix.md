``` py
import heapq


class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        result, heap = None, []
        
        count = 0
        
        for j in range(len(matrix)):
            heapq.heappush(heap, (matrix[j][0], j, 0))
        
        while count < k:
            result, j, i = heapq.heappop(heap)
                                         
            if i + 1 < len(matrix[0]):
                heapq.heappush(heap, (matrix[j][i+1], j, i+1))
            
            count += 1
            
        return result
```
