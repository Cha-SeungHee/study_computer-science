``` java
import java.util.*;

class Solution {
    int[] dx = {1, 0, -1, 0}; // right, up, left, down
    int[] dy = {0, -1, 0, 1};

    public int solution(int[][] maps) {
        return bfs(maps);
    }

    private int bfs(int[][] maps) {
        boolean[][] visited = new boolean[maps.length][maps[0].length];

        Queue<Node> queue = new LinkedList<>();

        queue.offer(new Node(0, 0));

        int count = 0;
        boolean exit = false;

        while (!queue.isEmpty()) {
            int size = queue.size();
            count = count + 1;

            for (int k = 0 ; k < size; k++) {
                Node node = queue.poll();

                if (node.y == maps.length - 1 && node.x == maps[0].length - 1) {
                    exit = true;
                    break;
                }

                for (int d = 0; d < 4; d++) {
                    int ny = node.y + dy[d];
                    int nx = node.x + dx[d];

                    if (isValid(ny, nx, maps) && !visited[ny][nx]) {
                        queue.offer(new Node(ny, nx));
                        visited[ny][nx] = true;
                    }
                }
            }

            if (exit) break;
        }

        return (exit) ? count : -1;
    }

    private boolean isValid(int y, int x, int[][] maps) {
        return 0 <= x && x <= maps[0].length - 1 && 0 <= y && y <= maps.length - 1 && maps[y][x] == 1;
    }
}

class Node {
    int y, x;

    Node (int y, int x) {
        this.y = y;
        this.x = x;
    }
}
```

기본 BFS. 응용 내용 


``` py
from collections import deque

def solution(maps):
    yLen = len(maps)
    xLen = len(maps[0])
    dx = [1, 0, -1, 0]
    dy = [0, -1, 0, 1]
    
    visited = [list(False for _ in range(xLen)) for _ in range(yLen)]
    
    count = 0
    found = False    
    queue = deque()
    queue.append((0, 0))    
    visited[0][0] = True
    
    while queue:
        size = len(queue)
        count += 1        
        
        for _ in range(size):
            y, x = queue.popleft()

            if y == yLen - 1 and x == xLen - 1:
                return count                

            for d in range(4):
                ny = y + dy[d]
                nx = x + dx[d]

                if ny < 0 or ny >= yLen or nx < 0 or nx >= xLen:
                    continue

                if visited[ny][nx] or maps[ny][nx] == 0:
                    continue

                visited[ny][nx] = True
                queue.append((ny, nx))
    
    return -1
```
