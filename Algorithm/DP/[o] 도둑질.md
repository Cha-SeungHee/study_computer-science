```` java
class Solution {
    public int solution(int[] money) {
        int max = Integer.MIN_VALUE;
        
        int[] dp = new int[money.length];
        
        // 첫 집 선택
        dp[0] = money[0];        
        dp[1] = money[0];
        
        for (int i = 2; i < money.length - 1; i++) {
            int bigger = Math.max(dp[i - 2] + money[i], dp[i - 1]);
            dp[i] = bigger;
        }
        
        max = Math.max(max, dp[money.length - 2]);
        
        // 첫 집 선택 x
        dp[0] = 0;        
        dp[1] = money[1];
        
        for (int i = 2; i < money.length; i++) {
            int bigger = Math.max(dp[i - 2] + money[i], dp[i - 1]);
            dp[i] = bigger;
        }
        
        max = Math.max(max, dp[money.length - 1]);        
        
        return max;
    }
}
````
