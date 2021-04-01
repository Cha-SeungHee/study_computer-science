``` py
class Solution:
    def isHappy(self, n: int) -> bool:
        num_set = set()
        num = n
        num_work = 0
    
        while num > 0:
            num_work += (num % 10) ** 2
            num = num // 10
            
            if num == 0:
                if num_work in num_set:
                    return False
                elif num_work == 1:
                    return True
                else:
                    num_set.add(num_work)
                    num = num_work       
                    num_work = 0
```
