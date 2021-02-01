```java  
class Solution {    
    public int numSquares(int n) {
        int[] dp = new int[n+1];    
        Arrays.fill(dp, -1);
        
        return numSquareHelper(n, dp);
    }
    
    private int numSquareHelper(int n, int[] dp) {
        if (n<=0) return 0;
        
        if (dp[n] > 0) return dp[n];
        
        int square = (int) Math.sqrt(n);
        int min = numSquareHelper(n-1, dp)+1;
        for (int i=1; i<=square; i++) {
            int tmp = numSquareHelper(n-i*i, dp)+1;
            min = Math.min(min, numSquareHelper(n-i*i, dp)+1);            
        }
        dp[n] = min;
        
        return dp[n];
    }
}
```
#### 확인
1. 해쉬맵을 쓸 때보다 배열을 쓸 때가 훨씬 속도가 빠르다. 실제 해쉬 계산 시간 때문인 것으로 


```java  
class Solution {    
    public int numSquares(int n) {
        HashMap<Integer, Integer> map = new HashMap<>();
        return numSquaresHelper(n, map);
    }
    
    private int numSquaresHelper(int n, HashMap<Integer, Integer> map) {
        if (n < 0) return Integer.MAX_VALUE;
        if (n==0) return 0;        
        
        if (map.containsKey(n)) return map.get(n);
        
        int root = (int) Math.sqrt(n);
        int min = Integer.MAX_VALUE;
        for (int i=1; i<=root; i++) {
            min = Math.min(min, numSquaresHelper(n-i*i, map)+1);
        }
        
        map.put(n, min);
        return min;
    }
}
```


#### 확인
1. squares인 경우 +1
2. Math.sqrt(n)의 return type은 double 
