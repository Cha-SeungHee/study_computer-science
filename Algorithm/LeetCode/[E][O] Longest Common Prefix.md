``` py
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if len(strs) == 0:
            return ""
        
        if len(strs) == 1:
            return strs[0]
        
        prefix = ""
        
        index = 0
        exist = True
        while exist:
            if len(strs[0]) == index:
                break
            
            letter = strs[0][index]
            for string in strs:
                if len(string) == index or string[index] != letter:
                    exist = False
                    break
                    
            if exist:
                prefix += letter
                index += 1
                
        return prefix
```
