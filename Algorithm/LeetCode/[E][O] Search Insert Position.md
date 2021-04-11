``` py
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        if target < nums[0]:
            return 0
        if target > nums[-1]:
            return len(nums)
        
        
        begin, end = 0, len(nums) - 1
            
        while begin <= end:
            mid = begin + (end - begin) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                end = mid - 1
            else:
                begin = mid + 1
            
        return begin
```
