``` py
import re
import itertools

def solution(expression):
    operators = list(itertools.permutations(['-', '+', '*'], 3))     
    expression = re.split('([-+*])', expression)
    
    results = []
    for operator in operators :
        exp = expression[:]            
        for op in operator :
            while op in exp :
                index = exp.index(op)
                exp[index - 1] = str(eval(exp[index - 1] + op + exp[index + 1]))
                del exp[index : index + 2]        
        results.append(abs(int(exp[0])))   
                       
    return max(results)
```
