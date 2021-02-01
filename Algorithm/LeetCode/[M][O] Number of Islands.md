``` java
class Solution {
    private int[] dx = {1, 0, -1, 0}; // right, up, left, down
    private int[] dy = {0, -1, 0, 1};
    private boolean[][] visited;
    private int yLen;
    private int xLen;
    
    public int numIslands(char[][] grid) {
        yLen = grid.length;
        xLen = grid[0].length;
        visited = new boolean[yLen][xLen];
        
        int numIsland = 0;
        
        for (int j = 0; j < yLen; j++) {
            for (int i = 0; i < xLen; i++) {
                if (!visited[j][i] && grid[j][i] == '1') {
                    bfs(grid, j, i);
                    numIsland = numIsland + 1;
                }
            }
        }
        
        
        return numIsland;
    }
    
    private void bfs(char[][] grid, int y, int x) {        
        visited[y][x] = true;
        Queue<Node> queue = new LinkedList<>();
        
        queue.offer(new Node(y, x));
        while (!queue.isEmpty()) {
            int size = queue.size();
            
            for (int k = 0; k < size; k++) {
                Node node = queue.poll();
                
                for (int dir = 0; dir < 4; dir++) {
                    int ny = node.y + dy[dir];
                    int nx = node.x + dx[dir];
                    
                    if (isValid(ny, nx) && grid[ny][nx] == '1') {
                        queue.offer(new Node(ny, nx));
                        visited[ny][nx] = true;
                    }
                }
            }
        }
    }
    
    private boolean isValid(int y, int x) {
        return 0 <= y && y <= yLen - 1 && 0 <= x && x <= xLen - 1 && !visited[y][x];
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
