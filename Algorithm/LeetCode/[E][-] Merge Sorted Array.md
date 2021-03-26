``` py
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        index, index1, index2 = m+n-1, m-1, n-1
        
        while index1 >=0 and index2 >= 0:
            if nums1[index1] >= nums2[index2]:
                nums1[index] = nums1[index1]
                index1 -= 1
            else:
                nums1[index] = nums2[index2]
                index2 -= 1            
            index -= 1
        
        while index2 >= 0:
            nums1[index] = nums2[index2]
            index -= 1
            index2 -= 1      
```
