``` py
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        contain = set()
        resultList = []
        
        def permuteHelper(nums, result):
            nonlocal contain, resultList
            
            if len(result) == len(nums):
                resultList.append(result[0:len(result)])
                return
        
            for num in nums:
                if num in contain:
                    continue
                else:
                    result.append(num)
                    contain.add(num)
                    permuteHelper(nums, result)
                    result.pop()
                    contain.remove(num)
        
        permuteHelper(nums, [])
        
        return resultList
```
