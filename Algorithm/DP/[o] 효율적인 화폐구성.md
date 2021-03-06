``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        st = new StringTokenizer(br.readLine(), " ");
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        int[] money = new int[N];
        int[] dp = new int[M + 1];

        for (int i = 0; i < N; i++) {
            money[i] = Integer.parseInt(br.readLine());
        }

        Arrays.fill(dp, Integer.MAX_VALUE);

        for (int i = 0; i < money.length; i++) {
            if (money[i] < M + 1) dp[money[i]] = 1;
        }

        for (int i = 1; i < M + 1; i++) {
            for (int j = 0; j < money.length; j++) {
                if (i + money[j] < M + 1 && dp[i] != Integer.MAX_VALUE) {
                    dp[i + money[j]] = Math.min(dp[i + money[j]], dp[i] + 1);
                }
            }
        }

        int ans = (dp[M] == Integer.MAX_VALUE) ? -1 : dp[M];

        System.out.println(ans);
    }
}
```

``` py
N, M = list(map(int, input().split()))
dp = [0] * (M + 1)
coin = []

for i in range(N):
    type = int(input())
    if type <= M:
        dp[type] = 1
        coin.append(type)

for i in range(M + 1):
    for c in coin:
        if i - c > 0 and dp[i - c] > 0:
            if dp[i] == 0:
                dp[i] = dp[i - c] + 1
            else:
                dp[i] = min(dp[i], dp[i - c] + 1)

print(dp)
print(-1 if dp[M] == 0 else dp[M])
```
