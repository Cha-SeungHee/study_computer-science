``` java
class Solution {
    int[] dp;
    
    public int numSquares(int n) {
        dp = new int[n + 1];
        
        for (int i = 1; i * i <= n; i++) {
            dp[i * i] = 1;
        }
        
        return numSquaresHelper(n, dp);
    }
    
    private int numSquaresHelper(int n, int[] dp) {
        if (n <= 0) return 0;
        
        if (dp[n] > 0) return dp[n];
        
        int min = Integer.MAX_VALUE;
        for (int i = 1; i * i <= n; i++) {
            int temp = numSquaresHelper(n - i * i, dp);
            if (temp != Integer.MAX_VALUE) min = Math.min(min, temp + 1);
        }
        
        return dp[n] = min;
    }
}
```

- 조금 더 빠른 코드 작성 필요  
- nuMSquaresHelper 내에서 i = 0부터 계산 시 무한 루프 빠질 수 있음  
