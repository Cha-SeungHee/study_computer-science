``` py
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        INF = 10**9
        result = INF
        dp = [[INF] * len(tri) for tri in triangle]
        
        dp[0][0] = triangle[0][0]
        for j in range(len(triangle) - 1):
            for i in range(len(triangle[j])):
                dp[j+1][i] = min(dp[j][i] + triangle[j+1][i], dp[j+1][i])
                dp[j+1][i+1] = min(dp[j][i] + triangle[j+1][i+1], dp[j+1][i+1])
            
        
        for num in dp[len(dp) - 1]:
            result = min(result, num)
                         
        return result 
```

최적화 시켜보기  
Follow up: Could you do this using only O(n) extra space, where n is the total number of rows in the triangle?
