Two Pointers
```java  
class Solution {
    public int rob(int[] nums) {      
        if (nums == null || nums.length == 0) return 0;
        
        int prevChosen = 0;
        int prevNotChosen = 0;
        
        int currentChosen = 0;
        int currentNotChosen = 0;
        
        for (int i=0; i<nums.length; i++) {
            currentChosen = prevNotChosen + nums[i];
            currentNotChosen = Math.max(prevChosen, prevNotChosen);
            
            prevChosen = currentChosen;
            prevNotChosen = currentNotChosen;
        }
        
        return Math.max(prevChosen, prevNotChosen);            
    }
}
``` 

DP 통과
```java  
class Solution {
    public int rob(int[] nums) {      
        int len = nums.length;
        if (len == 0) return 0;
        int[] dp = new int[len + 1];
        dp[0] = 0;
        dp[1] = nums[0];

        for (int i = 2; i <= len; i++){
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i - 1]);
        }
        return dp[len];
    }
}
``` 

DP 시간초과 (이유 잘 모르겠음)

```java  
class Solution {
    public int rob(int[] nums) {      
        if (nums.length ==0 || nums == null) return 0;
        
        int[] dp = new int[nums.length];
        Arrays.fill(dp, -1);        
        
        return robMax(nums.length-1, nums, dp);
    }
    
    private int robMax(int i, int[] nums, int[] dp) {
        if (i<0) return 0;
        if (dp[i] > 0) return dp[i];
        
        int max = Math.max(robMax(i-1, nums, dp), robMax(i-2, nums, dp) + nums[i]);
        dp[i] = max;
        
        return dp[i];
    }
}
``` 
