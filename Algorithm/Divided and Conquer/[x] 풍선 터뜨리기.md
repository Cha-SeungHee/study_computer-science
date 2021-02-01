``` java
import java.util.*;

class Solution {
    public int solution(int[] a) {
        HashSet<Integer> set = new HashSet<>();
        
        set.add(a[0]);
        set.add(a[a.length - 1]);
        
        int min = a[0];        
        for (int i = 1; i < a.length - 1; i++) {
            if (min > a[i]) {
                set.add(a[i]);
                min = a[i];
            }            
        }
        
        min = a[a.length - 1];
        for (int i = a.length - 2; i >= 1; i--) {
            if (min > a[i]) {
                set.add(a[i]);
                min = a[i];
            }
        }            
        
        return set.size();
    }
}
```

1. 한번의 큰 값을 터뜨리는 행위가 의미가 있는 경우는 최후의 두 숫자가 남았을 경우  
2. 최후의 두 숫자를 (최소값) 뽑을 수 있는 경우에 대해 고려  
