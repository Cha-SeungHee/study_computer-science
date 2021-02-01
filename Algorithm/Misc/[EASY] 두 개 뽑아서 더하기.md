``` java
import java.util.*;

class Solution {
    public int[] solution(int[] numbers) {
        HashSet<Integer> sumSet = new HashSet<>();
        
        for (int i = 0; i < numbers.length; i++) {
            for (int j = i + 1; j < numbers.length; j++) {
                sumSet.add(numbers[i] + numbers[j]);
            }
        }
        
        int index = 0;
        int[] answer = new int[sumSet.size()];        
        
        for (int sum : sumSet) {
            answer[index] = sum;
            index = index + 1;
        }        
        
        Arrays.sort(answer);
        
        return answer;
    }
}
```
