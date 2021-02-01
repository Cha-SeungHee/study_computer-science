``` java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0) return - 1;
        
        if (amount == 0) return 0;
        
        int[] dp = new int[amount + 1];
        
        for (int coin : coins) {
            if (coin <= amount) dp[coin] = 1;
        }
        
        int result = coinChangeHelper(dp, coins, amount);
        return (result == Integer.MAX_VALUE) ? -1 : result;
    }
    
    private int coinChangeHelper(int[] dp, int[] coins, int amount) {
        if (amount < 0) return Integer.MAX_VALUE;
        if (amount == 0) return 0;
        
        if (dp[amount] > 0) return dp[amount];
        
        int min = Integer.MAX_VALUE;
        for (int coin : coins) {
            if (coin > amount) continue;
            
            int temp = coinChangeHelper(dp, coins, amount - coin);
            if (temp != Integer.MAX_VALUE) min = Math.min(min, temp + 1);
        }
        
        return dp[amount] = min;
    }
}
```

- CoinChnageHelper를 쓴 이유: dp 매번 생성 x  
- amount - coin 했을 때 값이 음수가 나오는 경우는 계산 불가한 케이스임을 놓침 -> 별도 예외처리 해줌   
