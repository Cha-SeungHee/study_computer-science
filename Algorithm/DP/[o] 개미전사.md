``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine());
        int[] nums = new int[N];
        int[] dp = new int[N];

        st = new StringTokenizer(br.readLine(), " ");
        for (int i = 0; i < N; i++) {
            nums[i] = Integer.parseInt(st.nextToken());
        }

        /* Solution 1 */
        Arrays.fill(dp, -1);
        dp[0] = nums[0];
        dp[1] = nums[1];

        for (int i = 2; i < N; i++) {
            dp[i] = Math.max(dp[i], dp[i-2] + nums[i]);
            if (i - 3 >= 0) dp[i]= Math.max(dp[i], dp[i - 3] + nums[i]);
        }

        System.out.println(dp[N - 1]);

        /* Solution 2 */        
        Arrays.fill(dp, -1);
        dp[0] = nums[0];
        dp[1] = nums[1];

        for (int i = 2; i < N; i++) {
            dp[i] = Math.max(dp[i], dp[i - 1]);
            dp[i]= Math.max(dp[i], dp[i - 2] + nums[i]);
        }

        System.out.println(dp[N - 1]);
    }
}
```

``` py 
n = int(input())
food = list(map(int, input().split()))
dp = [0] * n

dp[0] = food[0]
dp[1] = max(dp[0], food[1])

for i in range(2, n):
    dp[i] = max(dp[i - 2] + food[i], dp[i - 1])

print(dp[n - 1])
```
