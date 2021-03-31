``` py
class Solution:
    def fizzBuzz(self, n: int) -> List[str]:
        num_list = []
        for i in range(1, n+1):
            if i % 3 == 0 and i % 5 == 0:
                num_list.append("FizzBuzz")
            elif i % 3 == 0:
                num_list.append("Fizz")
            elif i % 5 == 0:
                num_list.append("Buzz")
            else:
                num_list.append(str(i))
        
        return num_list
        
```
