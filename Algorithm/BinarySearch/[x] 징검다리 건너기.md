``` java
import java.util.*;

class Solution {
    public int solution(int[] stones, int k) {
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;

        for (int stone : stones) {
            min = Math.min(min, stone);
            max = Math.max(max, stone);
        }

        return search(stones, min, max, k);
    }

    int search(int[] stones, int min, int max, int k) {
        int begin = min, end = max;

        while (begin <= end) {
            int mid = begin + (end - begin) / 2;

            if (canCross(stones, mid, k)) {
                begin = mid + 1;
            } else {
                end = mid - 1;
            }
        }

        return begin - 1;
    }

    boolean canCross(int[] stones, int friends, int k) {
        boolean canCross = true;

        int count = 0;
        for (int stone : stones) {
            if (stone - friends < 0) {
                count = count + 1;
            } else {
                count = 0;
            }

            if (count >= k) {
                canCross = false;
                break;
            }
        }

        return canCross;
    }
}
```
