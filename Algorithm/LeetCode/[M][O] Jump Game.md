``` java
class Solution {
    public boolean canJump(int[] nums) {
        boolean[] dp = new boolean[nums.length];
        
        dp[nums.length - 1] = true;
        for (int i = nums.length - 2; i >= 0; i--) {
            for (int k = nums[i]; k >= 1; k--) {
                int index = i + k;
                
                if (index >= nums.length - 1 || dp[index]) {
                    dp[i] = true;
                    break;
                }            
            }
        }
        
        return dp[0];
    }
}
```
