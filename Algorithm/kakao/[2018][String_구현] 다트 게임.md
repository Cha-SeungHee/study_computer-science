``` java
import java.util.*;

class Solution {
    public int solution(String dartResult) {
        ArrayList<Integer> list = new ArrayList<>();
        
        int num = 0, sum = 0;
        for (int i = 0; i < dartResult.length(); i++) {
            char ch = dartResult.charAt(i);
            int index = 0;
            int temp = 0;
            
            switch (ch) {
                case '1', '2', '3', '4', '5', '6', '7', '8', '9':                                        
                    num = ch - '0';                    
                    break;
                    
                case '0':
                    num = num * 10;
                    break;
                    
                case 'S':     
                    list.add(num);                    
                    num = 0;
                    break;
                    
                case 'D':
                    num = (int) Math.pow(num, 2);   
                    list.add(num);
                    num = 0;
                    break;
                    
                case 'T':
                    num = (int) Math.pow(num, 3);      
                    list.add(num);                    
                    num = 0;
                    break;
                    
                case '#':                    
                    temp = list.get(list.size() - 1);
                    list.set(list.size() - 1, -1 * temp);
                    break;
                    
                case '*':
                    index = list.size() - 2;
                    temp = 0;
                    if (index >= 0) {
                        temp = list.get(index);
                        list.set(index, 2 * temp);
                    } 
                    
                    temp = list.get(list.size() - 1);
                    list.set(list.size() - 1, 2 * temp);
                    break;
                    
                default :
                    break;
            }
        }
        
        for (int number : list) {
            sum = sum + number;
        }
        
        return sum;
    }
}
```

``` py
import re

def solution(dartResult):
    sum = 0
    resultList = []
    
    map = {'S' : '**1', 'D' : '**2', 'T' : '**3', '#' : '*-1'}
    
    scoreList = re.sub("(\d+)", " \g<1>", dartResult).split()
    
    for score in scoreList :
        for char in score :
            score = score.replace(char, map.get(char, char))                        
        if score[-1] == '*' :
            score += '2'        
            if resultList :
                resultList[-1] += '*2'                            
        resultList.append(score)
    
    for result in resultList :
        sum += eval(result)
    
    return sum 
```
