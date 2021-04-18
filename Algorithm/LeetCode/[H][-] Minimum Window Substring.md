``` py
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        count = len(t)
        have = {}
        need = {}
        
        for letter in t:
            need[letter] = need.get(letter, 0) + 1
        
        for key in need.keys():
            have[key] = 0
            
        countNeed = len(need.keys())
        countHave = 0
        
        begin = end = 0
        condition = False
        output = ""
        
        while end < len(s):
            if s[end] in need:
                have[s[end]] += 1
                if have[s[end]] == need[s[end]]:
                    countHave += 1
                
                if countHave >= countNeed:
                    condition = True
                
            while condition:        
                if not output or (output and len(output) > len(s[begin:end+1])):
                    output = s[begin:end+1]
                    
                if s[begin] in need:
                    have[s[begin]] -= 1
                    if have[s[begin]] < need[s[begin]]:
                        countHave -= 1
                    
                    if countHave < countNeed:
                        condition = False
                
                begin += 1
            
            end += 1
                
        return output
```
