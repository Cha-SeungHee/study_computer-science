```java  
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount+1];
        
        Arrays.fill(dp, -1);        
        for (int coin : coins) {
            if (0 < coin && coin <= amount) {
                dp[coin] = 1;
            }
        }
        
        int ans = helper(coins, amount, dp);
        return (ans == Integer.MAX_VALUE) ? -1 : ans;
    }
    
    private int helper(int[] coins, int amount, int[] dp) {
        if (dp[amount] > 0) return dp[amount];
        
        if (amount <=0) return 0;
        
        int min = Integer.MAX_VALUE;
        for (int coin : coins) {
            if (coin <= amount) {
                int tmp = helper(coins, amount-coin, dp);
                if (tmp > 0 && tmp != Integer.MAX_VALUE) min = Math.min(min, tmp+1);
            }
        }        
        
        dp[amount] = min;
        
        return min;
    }
}
```  

#### 확인
1. return 값이 Integer.MAX_VALUE 값이 나오더라도 저장을 해줘야 한다. (실패한 케이스도 cache 해놔야겠지)
