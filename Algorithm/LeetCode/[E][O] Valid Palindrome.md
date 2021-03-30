``` py
import re

class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = re.sub("[^a-zA-Z0-9]", "", s)
        s = s.lower()
        
        begin, end = 0, len(s)-1
        
        while begin <= end:
            if s[begin] != s[end]:
                return False
            begin += 1
            end -= 1
            
        return True
```
