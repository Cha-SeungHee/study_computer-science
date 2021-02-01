``` java
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        
        dp[0] = 1;
        
        for (int i = 1; i <= n; i++) {
            for (int k = 0; k < i; k++) {
                dp[i] += dp[k] * dp[i - k - 1];
            }
        }
        
        return dp[n];
    }
}
```
