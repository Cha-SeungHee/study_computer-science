``` java
class Solution {
    int[] dx = {1, 0, -1, 0}; // right, up, left, down
    int[] dy = {0, -1, 0, 1};
    
    public boolean exist(char[][] board, String word) {
        boolean result = false;
        boolean[][] visited = new boolean[board.length][board[0].length];
        
        for (int j = 0; j < board.length; j++) {
            for (int i = 0; i < board[0].length; i++) {
                visited[j][i] = true;                
                result = dfs(j, i, 0, visited, board, word);
                visited[j][i] = false;
                
                if (result) return true;
            }
        }
        
        return false;
    }
    
    private boolean dfs(int y, int x, int index, boolean[][] visited, char[][] board, String word) {
        if (index == word.length() - 1 && word.charAt(index) == board[y][x]) return true;        
        if (board[y][x] != word.charAt(index)) return false;
        
        boolean result = false;
        
        for (int k = 0; k < 4; k++) {
            int nx = x + dx[k];
            int ny = y + dy[k];
            
            if (isValid(ny, nx, board) && !visited[ny][nx]) {
                visited[ny][nx] = true;
                result = dfs(ny, nx, index + 1, visited, board, word);
                visited[ny][nx] = false;
                
                if (result) break;
            }
        }
        
        return result;
    }
    
    private boolean isValid(int y, int x, char[][] board) {
        return 0 <= y && y <= board.length - 1 && 0 <= x && x <= board[0].length - 1;
    }
}
```
