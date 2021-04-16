``` py
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key = lambda i : (i[0], i[1]))
        
        result = [intervals[0]]
        
        for start, end in intervals[1:]:
            if result[-1][1] >= start:
                result[-1][1] = max(result[-1][1], end)
            else:
                result.append([start, end])
        
        return result
```
