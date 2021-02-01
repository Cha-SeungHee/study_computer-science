``` java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if (triangle == null || triangle.size() == 0) return 0;
        
        int depth = triangle.size();
        
        int[][] dp = new int[depth][depth];
        
        for (int j = 0; j < depth; j++) {
            for (int i = 0; i < depth; i++) {
                dp[j][i] = Integer.MAX_VALUE;
            }
        }
        
        for (int i = 0; i < depth; i++) {
            dp[depth - 1][i] = triangle.get(depth - 1).get(i);
        }
        
        for (int j = depth - 2; j >= 0; j--) {
            for (int i = 0; i <= j; i++) {
                dp[j][i] = triangle.get(j).get(i) + Math.min(dp[j + 1][i], dp[j + 1][i + 1]);
            }
        }
        
        return dp[0][0];
    }
}
```
