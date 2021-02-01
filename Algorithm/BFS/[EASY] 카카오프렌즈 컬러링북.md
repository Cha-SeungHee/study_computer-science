``` java
import java.util.*;

class Solution {
    boolean[][] visited;
    int[][] board;
    
    int[] dx = {1, 0, -1, 0}; // right, up, left, down
    int[] dy = {0, -1, 0, 1};
    int xLen;
    int yLen;
    
    public int[] solution(int m, int n, int[][] picture) {
        board = picture;
        yLen = m;
        xLen = n;
        visited = new boolean[yLen][xLen];
        
        int numRegion = 0;
        int maxRegion = Integer.MIN_VALUE;
        
        for (int j = 0; j < m; j++) {
            for (int i = 0; i < n; i++) {
                if (!visited[j][i] && board[j][i] != 0) {
                    int size = bfs(j, i);
                    numRegion = numRegion + 1;
                    maxRegion = Math.max(maxRegion, size);
                }
            }
        }
        
        int[] answer = new int[2];
        answer[0] = numRegion;
        answer[1] = maxRegion;
        
        return answer;
    }
    
    private int bfs(int j, int i) {
        int area = 0;
        
        Queue<Point> queue = new LinkedList<>();
        
        queue.offer(new Point(j, i));
        visited[j][i] = true;                
        
        while (! queue.isEmpty()) {
            Point point = queue.poll();
            area = area + 1;
            
            for (int k = 0; k < 4; k++) {
                int nx = point.x + dx[k];
                int ny = point.y + dy[k];
                
                if (isValid(nx, ny) && !visited[ny][nx] && board[ny][nx] == board[point.y][point.x]) {
                    queue.offer(new Point(ny, nx));
                    visited[ny][nx] = true;
                }
            }
        }
        
        return area;
    }
    
    private boolean isValid(int x, int y) {
        return 0 <= x && x <= xLen - 1 && 0 <= y && y <= yLen - 1;
    }
}

class Point {
    int y, x;
    
    Point(int y, int x) {
        this.y = y;
        this.x = x;
    }
}
```
