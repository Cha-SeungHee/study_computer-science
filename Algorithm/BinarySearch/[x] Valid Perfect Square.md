```java  
class Solution {
    public boolean isPerfectSquare(int num) {       
        long start = 1;
        long end = num;        
        
        while (start <= end) {
            long mid = start + (end-start)/2;
            
            if (mid*mid == num) {
                return true;
            }
            if (mid*mid > num) {
                end = mid-1;
            } else {
                start = mid+1;
            }
        }
        
        return false;
    }
}
```

#### 확인
0. 풀이 방법 생각 못함
1. long type 안썼을 때 overflow 발생



#### long type 안쓰는 solution
```java  
class Solution {
    public boolean isPerfectSquare(int num) {
        int left = 1, right = num;
        while (left <= right) {
            int mid = left + (right - left) / 2; // to avoid overflow incase (left+right)>2147483647
            int res = num / mid, remain = num % mid;
            if (res == mid && remain == 0) return true; // check if mid * mid == num
            if (res > mid) { // mid is small -> go right to increase mid
                left = mid + 1;
            } else {
                right = mid - 1; // mid is large -> to left to decrease mid
            }
        }
        return false;
    }
}
```
