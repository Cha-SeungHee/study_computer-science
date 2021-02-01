``` java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix == null) return 0;
        
        int rows = matrix.length;
        int cols = matrix[0].length;
        int max = 0;
        
        int[][] dp = new int[rows][cols];
        
        for (int i = 0; i < cols; i++) {
            dp[0][i] = (matrix[0][i] == '1') ? 1 : 0;
            max = Math.max(max, dp[0][i]);
        }
        
        for (int j = 0; j < rows; j++) {
            dp[j][0] = (matrix[j][0] == '1') ? 1 : 0;
            max = Math.max(max, dp[j][0]);
        }
        
        for (int j = 1; j < rows; j++) {
            for (int i = 1; i < cols; i++) {
                if (matrix[j][i] == '1') {
                    dp[j][i] = Math.min(dp[j - 1][i - 1], Math.min(dp[j - 1][i], dp[j][i - 1])) + 1;
                    max = Math.max(max, dp[j][i]);    
                }
            }
        }
        
        return max * max;
    }
}
```
