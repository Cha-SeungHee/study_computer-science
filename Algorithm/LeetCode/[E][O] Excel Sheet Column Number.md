``` py
class Solution:
    def titleToNumber(self, columnTitle: str) -> int:
        result = 0
        
        dictionary = {}
        for i in range(26):
            dictionary[chr(ord('A')+i)] = i+1        
        
        for i in range(len(columnTitle)):
            result += 26**(len(columnTitle)-(i+1)) * dictionary[columnTitle[i]]
            
        return result            
```
