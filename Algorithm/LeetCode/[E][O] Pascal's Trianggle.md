``` py
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        result = [[] for _ in range(numRows)]
        
        for i in range(numRows):
            if i == 0:
                result[i].append(1)
            else:                
                result[i].append(result[i-1][0])
                for index in range(len(result[i-1])-1):
                    result[i].append(result[i-1][index] + result[i-1][index+1])
                result[i].append(result[i-1][-1])
                    
        return result
```
