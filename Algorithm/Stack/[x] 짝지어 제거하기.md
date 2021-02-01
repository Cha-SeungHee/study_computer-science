``` java
import java.util.*;

class Solution
{
    public int solution(String s)
    {
        int sLen = s.length();
        Stack<Character> stack = new Stack<>();
        
        for (int i = 0; i < sLen; i++) {
            char ch = s.charAt(i);
            
            if (!stack.isEmpty() && ch == stack.peek()) {
                stack.pop();
            } else {
                stack.push(ch);
            }
            
        }
        
        return (stack.isEmpty()) ? 1 : 0;
    }
}
``` 

스택으로 풀어야 한다는 사실을 생각하지 못함  
