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

``` py
class Solution:
    def numTrees(self, n: int) -> int:
        numTrees = [1] * (n + 1)
        
        for nodes in range(2, n+1):
            total = 0
            for root in range(1, nodes + 1):
                left = root - 1
                right = nodes - root
                total += numTrees[left] * numTrees[right]            
            numTrees[nodes] = total
                
        return numTrees[n]
```
