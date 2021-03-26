``` py
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if len(needle) == 0: 
            return 0
    
        for i in range(len(needle)-1, len(haystack)):           
            if haystack[i-len(needle)+1:i+1] == needle:
                return i-len(needle)+1
        
        return -1
```
