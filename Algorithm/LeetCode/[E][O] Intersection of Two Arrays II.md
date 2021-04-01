``` py
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        intersection = []
        dictionary = {}
        
        for num in nums1:
            dictionary[num] = dictionary.get(num, 0) + 1
        
        for num in nums2:
            if num in dictionary and dictionary[num] > 0:
                intersection.append(num)
                dictionary[num] -= 1
            
        return intersection        
```
