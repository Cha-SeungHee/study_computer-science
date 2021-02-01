``` java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        if (T == null || T.length == 0) return new int[]{};
        
        Stack<Temperature> stack = new Stack<>();
        int[] dayToWarm = new int[T.length];
        
        for (int i = 0; i < T.length; i++) {
            if (stack.isEmpty()) {
                stack.push(new Temperature(T[i], i));
                continue;
            }
            
            int count = 0;
            
            if (stack.peek().temperature >= T[i]) {
                stack.push(new Temperature(T[i], i));
            } else {
                while (!stack.isEmpty() && stack.peek().temperature < T[i]) {
                    Temperature temp = stack.pop();    
                    
                    dayToWarm[temp.day] = i - temp.day;
                }
                
                stack.push(new Temperature(T[i], i));            
            }
        }
        
        return dayToWarm;
    }
    
    class Temperature {
        int temperature;
        int day;
        
        Temperature (int temperature, int day) {
            this.temperature = temperature;
            this.day = day;
        }
    }
}
```
