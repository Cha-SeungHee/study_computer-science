``` py
class Solution:
    def mySqrt(self, x: int) -> int:
        if x == 0:
            return 0
        
        begin = 1
        end = x
        
        while begin <= end:
            mid = begin + (end-begin)//2
            
            if mid**2 == x:
                return mid
            
            if (mid-1)**2 <= x and mid**2 > x:
                return mid-1
            
            if (mid-1)**2 > x:
                end = mid-1
            if mid**2 < x:
                begin = mid+1
```

``` py
class Solution:
    def mySqrt(self, x: int) -> int:        
        left, right = 0, x
        
        while left <= right:            
            mid = left + (right - left) // 2
            square = mid ** 2
            
            if square <= x:
                left = mid + 1
            
            elif square > x :
                right = mid -1            
        
        return left-1
```
