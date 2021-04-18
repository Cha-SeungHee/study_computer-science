``` py
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        result = []
        
        for i in range(1 << len(nums)):
            subset = []
            
            tmp = i
            index = 0
            while tmp > 0:
                if tmp & 1 == 1:
                    subset.append(nums[index])
                tmp >>= 1
                index += 1
            
            result.append(subset[:])
            
        return result
```
