``` java
import java.util.*;

class Solution {
    public int[] solution(String s) {
        int countZero = 0;
        int countConvert = 0;
        
        int[] answer = new int[2];
        
        while (!s.equals("1")) {    
            countConvert = countConvert + 1;
            
            int lengthBefore = s.length();              
            
            s = s.replaceAll("0", "");            
            
            int lengthAfter = s.length();
            
            countZero = countZero + Math.abs(lengthBefore - lengthAfter);
            
            s = convertToBinary(lengthAfter);
        }        
        
        answer[0] = countConvert;
        answer[1] = countZero;
        
        return answer;
    }
    
    private String convertToBinary(int n) {
        StringBuilder sb = new StringBuilder();
        
        while (n > 0) {
            sb.append(n % 2);
            
            n = n / 2;
        }
        
        return sb.reverse().toString();
    }
}
```

- replace vs replaceAll
