#### Bottom-up
```` java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();

        int[] T = new int[N + 1];
        int[] P = new int[N + 1];
        int[] dp = new int[N + 2];
        int max = 0;

        for (int i = 1; i <= N; i++) {
            T[i] = sc.nextInt();
            P[i] = sc.nextInt();
        }

        dp[N + 1] = 0;

        for (int i = N; i >= 1; i--) {
            int time = T[i] + i;

            if (time <= N + 1) {
                dp[i] = Math.max(dp[time] + P[i], max);
                max = dp[i];
            }
            dp[i] = max;
        }

        System.out.println(max);
    }
}
````

#### Top-down
``` java
import java.util.*;
import java.io.*;

class Main {
    static int N;
    static int[] T;
    static int[] P;
    static int[][] dp;

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        N = Integer.parseInt(br.readLine());
        T = new int[N + 1];
        P = new int[N + 1];
        dp = new int[N + 1][N + 1];

        for (int j = 0; j <= N; j++) {
            for (int i = 0; i <= N; i++) {
                dp[j][i] = -1;
            }
        }

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            T[i] = Integer.parseInt(st.nextToken());
            P[i] = Integer.parseInt(st.nextToken());
        }

        int ans = dfs(0, 1);

        bw.write(ans + "\n");
        bw.flush();

        br.close();
        bw.close();
    }

    private static int dfs(int work, int day) {
        if (day == N + 1) {
            return 0;
        }

        if (dp[work][day] > 0) return dp[work][day];

        int money = -1;
        if (work == 0 && day + T[day] - 1 < N + 1) {
            int maxMoney = Math.max(dfs(T[day] - 1, day + 1) + P[day], dfs(0, day + 1));
            money = Math.max(money, maxMoney);
        } else {
            money = dfs(Math.max(0, work - 1), day + 1);
        }

        return dp[work][day] = money;
    }
}
```
