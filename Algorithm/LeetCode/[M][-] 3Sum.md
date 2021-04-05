``` py
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        
        result_set = set()
        searched = set()        
        for i in range(len(nums)-2):
            if nums[i] not in searched:
                result = []
                
                self.twoSum(nums, i + 1, len(nums) - 1, -nums[i], result)        
                if result:                    
                    for r in result:                        
                        new_result = [nums[i]]
                        new_result.extend(r)
                        result_set.add(tuple(new_result))
                searched.add(nums[i])
        
        return [list(s) for s in result_set]
        
    
    def twoSum(self, nums, begin, end, target, result):
        while begin < end:
            sum = nums[begin] + nums[end]
            if sum == target:         
                result.append([nums[begin], nums[end]])
                begin += 1
                end -= 1
            elif sum < target:
                begin += 1
            else: 
                end -= 1
```
