``` java
import java.util.*;

class Solution {
    public int solution(String s) {
        if (s.length() == 1) return 1;
        
        int min = 1000;         
        
        for (int sLen = 1; sLen <= s.length() / 2; sLen++) {            
            StringBuilder sb = new StringBuilder();
            int count = 1;
            String current = s.substring(0, sLen);                        
            
            for (int i = sLen; i < s.length(); i = i + sLen) {                
                String string = "";
                if (i + sLen > s.length()) {                    
                    string = s.substring(i, s.length());
                } else {
                    string = s.substring(i, i + sLen);
                }
                
                if (current.equals(string)) {
                    count = count + 1;
                } else {
                    if (count > 1) sb.append(count);
                    sb.append(current);

                    current = string;
                    count = 1;
                }                
            }
            
            if (count > 1) sb.append(count);
            sb.append(current);
            
            min = Math.min(min, sb.length());            
        }
        
        return min;
    }
}
```

```java 
import java.util.*;

class Solution {
    public int solution(String s) {
        if (s.length() == 1) return 1;
        
        int sLen = s.length();
        StringBuilder sb;
        int min = Integer.MAX_VALUE;
        
        for (int len=1; len<=sLen/2; len++) {
            String cur = "";
            int count = 1;
            sb = new StringBuilder();            
            
            for (int i=0; i<sLen; i=i+len) {                
                if (i==0) {
                    cur = s.substring(i, i+len);                    
                } else {
                    String newString;
                    if (i+len >= sLen) {
                        newString = s.substring(i, sLen);
                    } else {
                        newString = s.substring(i, i+len);    
                    }                    
                    
                    if (cur.equals(newString)) {
                        count = count+1;
                    } else {                        
                        if (count>1) sb.append(count);
                        sb.append(cur);                        
                        
                        cur = newString;
                        count = 1;
                    }        
                }
            }
            if (count>1) sb.append(count);
            sb.append(cur);            
            
            min = Math.min(min, sb.toString().length());            
        }        
                
        return min;
    }
}
``` 

#### 확인
1. 항상 예외처리
