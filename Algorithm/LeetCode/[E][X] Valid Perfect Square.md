``` java
class Solution {
    public boolean isPerfectSquare(int num) {
        long start = 1, end = num;
        
        while (start <= end) {
            long mid = start + (end - start) / 2;
            
            if (mid * mid == num) return true;
            
            if (mid * mid > num) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        
        return false;
    }
}
```

- 1 <= num <= 2^31 - 1 -> int의 범위는 음과 양을 모두 포함하기에 long  
- binary search  
