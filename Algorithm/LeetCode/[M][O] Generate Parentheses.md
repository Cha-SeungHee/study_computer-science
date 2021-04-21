``` py
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        result = []         
        bracket = []
        
        def dfs(countOpen, countClose):
            if countClose == n:
                result.append("".join(bracket))                
                return
        
            if countOpen < n:
                bracket.append('(')
                countOpen += 1
                dfs(countOpen, countClose)
                bracket.pop()
                countOpen -= 1
            
            if countOpen > countClose:
                bracket.append(')')
                countClose += 1
                dfs(countOpen, countClose)
                bracket.pop()
                countClose -= 1
            
        dfs(0,0)
        
        return result
```
