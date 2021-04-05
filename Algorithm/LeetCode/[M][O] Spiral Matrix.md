``` py
# right, down, left, up
dx = [1, 0, -1, 0] 
dy = [0, 1, 0, -1]


class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        result = [matrix[0][0]]
        
        MAX_COUNT = len(matrix[0]) * len(matrix)
        
        visited = [[False for _ in range(len(matrix[0]))] for _ in range(len(matrix))]
        visited[0][0] = True
        direction = 0
        current = [0, 0]            
        count = 1
        
        while count < MAX_COUNT:
            nx = current[0] + dx[direction]
            ny = current[1] + dy[direction]
            
            if count == MAX_COUNT:
                break
                
            if (nx >= len(matrix[0]) or ny >= len(matrix)) or visited[ny][nx]:
                direction = (direction + 1) % 4                
                continue
            else:
                current[0] = nx
                current[1] = ny
                visited[ny][nx] = True
                count += 1      
                result.append(matrix[ny][nx])
        
        return result        
```
