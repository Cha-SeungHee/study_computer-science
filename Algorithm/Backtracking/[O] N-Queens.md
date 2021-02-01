```java  
class Solution {
    public List<List<String>> solveNQueens(int n) {
        if (n==0) return null;
        
        List<List<String>> list = new ArrayList<>();
        boolean[] xvisited = new boolean[n];
        int[] queens = new int[n];
        solveNQueensHelper(list, xvisited, queens, 0, n);
        
        return list;        
    }
    
    private void solveNQueensHelper(List<List<String>> list, boolean[] xvisited, int[] queens, int row, int n) {
        if (row == n) {     
            List<String> tmp = new ArrayList<>();
            for (int j=0; j<queens.length; j++) {
                StringBuilder sb = new StringBuilder();
                for (int k=0; k<n; k++) {
                    if (k != queens[j]) {
                        sb.append(".");
                    } else {
                        sb.append("Q");
                    }
                }
                tmp.add(sb.toString());
            }
            list.add(tmp);
        }
        
        for (int i=0; i<n; i++) {
            if (!xvisited[i] && !isDiagonal(queens, row, i, row)) {
                xvisited[i] = true;
                queens[row] = i;
                solveNQueensHelper(list, xvisited, queens, row+1, n);
                xvisited[i] = false;
                queens[row] = 0;
            }
        }
    }
    
    private boolean isDiagonal(int[]queens, int row, int x, int y) {
        boolean diagonal = false;
        for (int k=0; k<row; k++) {
            int deltaX = Math.abs(queens[k] - x);
            int deltaY = Math.abs(k - y);                        
            if (deltaX == deltaY) {
                diagonal = true;
                break;
            }
        }
        
        return diagonal;
    }
    
    private class Point {
        int x;
        int y;
        
        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
}
```

#### 확인
1. 한번의 순회로 같은 열 또는 대각선에 이미 값이 존재하는지 확인했다면 공간활용도를 줄일 수 있었을 것
