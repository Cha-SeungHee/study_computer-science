``` java
import java.util.*;

class Solution {
    public int solution(int n) {
        String reverse = reverseTertiary(n);

        int len = reverse.length();
        int sum = 0;

        for (int i = 0; i < len; i++) {
            sum = sum + (int)Math.pow(3, i) * Integer.parseInt(reverse.substring(i, i + 1));
        }

        return sum;
    }

    private String reverseTertiary(int n) {
        StringBuilder sb = new StringBuilder();

        while (n > 0) {
            sb.append(n % 3);
            n = n / 3;
        }

        return sb.reverse().toString();
    }
}
```
