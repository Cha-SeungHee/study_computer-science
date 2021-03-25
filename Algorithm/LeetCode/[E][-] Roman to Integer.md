``` py
import re

class Solution:
    def romanToInt(self, s: str) -> int:
        symbol_dict = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500, 'M':1000}
        sub_list = {'IV', 'IX', 'XL', 'XC', 'CD', 'CM'}        
        s_list = re.split('(IV|IX|XL|XC|CD|CM)', s)
        
        result = 0     
        for string in s_list:
            if len(string) >= 2:
                if string in sub_list:
                    result += (symbol_dict[string[1]] - symbol_dict[string[0]])            
                else :
                    for letter in string:
                        result += symbol_dict[letter]
            else:
                result += symbol_dict.get(string, 0)        
        
        return result
```
