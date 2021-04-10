``` py
class Solution:
    def longestPalindrome(self, s: str) -> str:
        result = s[0]
        
        for i in range(len(s)):
            # odd number of letters
            l, r = i - 1, i + 1
            while l >= 0 and r <= len(s) - 1:
                if s[l] == s[r]:
                    if r - l + 1 > len(result):
                        result = s[l:r+1]
                else:
                    break
                l -= 1
                r += 1
            
            # even number of letters
            l, r = i, i + 1
            while l >= 0 and r <= len(s) - 1:
                if s[l] == s[r]:
                    if r - l + 1 > len(result):
                        result = s[l:r+1]
                else:
                    break
                l -= 1
                r += 1
        
        return result
```
