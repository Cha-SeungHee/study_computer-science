``` py
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        begin = self.binarySearchBias(nums, target, True)
        end = self.binarySearchBias(nums, target, False)
        
        return [begin, end]
    
    
    def binarySearchBias(self, nums, target, leftBias):
        begin, end = 0, len(nums) - 1
        index = -1
        
        while begin <= end:            
            mid = begin + (end - begin) // 2
            
            if target > nums[mid]:
                begin = mid + 1
            elif target < nums[mid]:
                end = mid - 1
            else:
                index = mid
                if leftBias:
                    end = mid - 1
                else:
                    begin = mid + 1
        
        return index
```
