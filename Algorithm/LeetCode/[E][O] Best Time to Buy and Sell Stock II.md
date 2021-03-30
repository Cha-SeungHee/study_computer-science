``` py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        stack = []
        
        for num in prices:
            if not stack:
                stack.append(num)
            else:
                if num >= stack[-1]:
                    stack.append(num)
                else:
                    profit += stack[-1] - stack[0]
                    stack = [num]
         
        if len(stack) > 1:
            profit += stack[-1] - stack[0]
        
        return profit                    
```
