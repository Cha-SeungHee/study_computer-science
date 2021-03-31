``` py
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        letters = {}
        for i in range(len(s)):
            letters[s[i]] = letters.get(s[i], 0) + 1
        
        for i in range(len(t)):
            letters[t[i]] = letters.get(t[i], 0) - 1
        
        for key in letters.keys():
            if letters[key] > 0:
                return False
        
        return True
```
