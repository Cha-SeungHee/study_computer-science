1. String to int array
``` py
numString = input()
nums = [numString[i:i+1] for i in range(len(numString))]
```

2. Character list to array
``` py
''.join(result)
```

3. Backtracking (append, del)
``` py
def calculate(index, maxLength, result):
    global maxNum

    if index == maxLength:
        maxNum = max(eval(''.join(result)), maxNum)
        return

    for j in range(len(oper)):
        if len(result) > 0:
            result.append(oper[j])
        result.append(nums[index])
        calculate(index + 1, maxLength, result)
        if len(result) > 1:
            del result[-1]
        del result[-1]
```
