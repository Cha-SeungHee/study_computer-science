``` py 
class Solution:
    def numSubseq(self, nums: List[int], target: int) -> int:
        nums.sort()
        result = 0
        MOD = 10**9 + 7
        
        r = len(nums) - 1
        for i, left in enumerate(nums):
            while (left + nums[r]) > target and i <= r:
                r -= 1
            
            if i <= r:
                result += (2**(r - i))
                result %= MOD
        
        return result
```
