``` java
class Solution {
    public int longestOnes(int[] A, int K) {
        int start = 0, end = 0, numZero = 0, max = Integer.MIN_VALUE;        
        
        while (end < A.length) {
            if (A[end] == 0) numZero = numZero + 1;
            
            while (numZero > K) {
                if (A[start] == 0) numZero = numZero - 1;
                
                start = start + 1;
            }
            
            max = Math.max(max, end - start + 1);
            
            end = end + 1;
        }
        
        return max;        
    }
}
```
