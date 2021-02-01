#### 시간초과 코드
``` java
import java.util.*;

class Main {
    public static void main(String[] args) {
        String[] strs = {"ba","na","n","a"};

        Solution solution = new Solution();
        System.out.println(solution.solution(strs, "banana"));
    }
}

class Solution {
    int min = Integer.MAX_VALUE;

    HashMap<Integer, ArrayList<String>> map;

    public int solution(String[] strs, String t) {
        int tLen = t.length();

        map = new HashMap<>();

        for (int i = 0; i < tLen; i++) {
            map.put(i, new ArrayList<>());
        }

        for (String s : strs) {
            int sLen = s.length();

            for (int i = 0; i < tLen; i++) {
                if (i + sLen <= tLen && s.equals(t.substring(i, i + sLen))) {
                    map.get(i).add(s);
                }
            }
        }

        backtrack(0, tLen, 0);

        return (min == Integer.MAX_VALUE) ? -1 : min;
    }

    void backtrack(int index, int length, int count) {
        if (index >= length) {
            min = Math.min(min, count);
            return;
        }

        ArrayList<String> list = map.get(index);

        for (String string : list) {
            backtrack(index + string.length(), length, count + 1);
        }
    }
}
```

### DP
```java
import java.util.*;

class Solution {
    HashMap<Integer, ArrayList<String>> map;
    int[] dp;

    public int solution(String[] strs, String t) {
        int tLen = t.length();
        dp = new int[tLen];
        map = new HashMap<>();

        Arrays.fill(dp, -1);

        for (int i = 0; i < tLen; i++) {
            map.put(i, new ArrayList<>());
        }

        for (String s : strs) {
            int sLen = s.length();

            for (int i = 0; i < tLen; i++) {
                if (i + sLen <= tLen && s.equals(t.substring(i, i + sLen))) {
                    map.get(i).add(s);
                }
            }
        }

        int result = dp(0, tLen);

        return (result == Integer.MAX_VALUE) ? -1 : result;
    }

    int dp(int index, int length) {
        if (index >= length) {
            return 0;
        }

        if (dp[index] > 0) return dp[index];

        ArrayList<String> list = map.get(index);

        int min = Integer.MAX_VALUE;

        for (String string : list) {
            int result = dp(index + string.length(), length);

            if (result != Integer.MAX_VALUE) min = Math.min(min, dp(index + string.length(), length) + 1);
        }

        return dp[index] = min;
    }
}
```
