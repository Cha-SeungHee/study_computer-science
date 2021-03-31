``` py
class Solution:
    def firstUniqChar(self, s: str) -> int:
        count = {}
        
        for letter in s:
            count[letter] = count.get(letter, 0) + 1
        
        for index in range(len(s)):
            if count[s[index]] == 1:
                return index
            
        return -1
```
