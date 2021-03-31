``` py
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        nums = [i+1 for i in nums]        
        
        for num in nums:            
            index = abs(num)-1
            if index == len(nums): 
                continue
            else:                
                nums[index] *= -1        
        
        for index in range(len(nums)):
            if nums[index] > 0:
                return index
        
        return len(nums)
```
