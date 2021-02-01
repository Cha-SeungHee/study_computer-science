#### Bottom-up
``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int testCase = Integer.parseInt(br.readLine());
        for (int i = 0; i < testCase; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            int N = Integer.parseInt(st.nextToken());
            int M = Integer.parseInt(st.nextToken());

            int[][] nums = new int[N][M];
            int[][] dp = new int[N][M];

            st = new StringTokenizer(br.readLine(), " ");
            for (int j = 0; j < N; j++) {
                for (int k = 0; k < M; k++) {
                    nums[j][k] = Integer.parseInt(st.nextToken());
                }
            }

            for (int j = 0; j < N; j++) {
                for (int k = 0; k < M; k++) {
                    dp[j][k] = -1;
                }
            }

            for (int j = 0; j < N; j++) {
                dp[j][0] = nums[j][0];
            }

            for (int k = 0; k < M - 1; k++) {
                for (int j = 0; j < N; j++) {
                    for (int l = -1; l <= 1; l++) {
                        if (0 <= j + l && j + l < N) {
                            dp[j + l][k + 1] = Math.max(dp[j + l][k + 1], dp[j][k] + nums[j + l][k + 1]);
                        }
                    }
                }
            }

            int max = Integer.MIN_VALUE;
            for (int j = 0; j < N; j++) {
                max = Math.max(max, dp[j][M - 1]);
            }
            System.out.println(max);
        }
    }
}

```

#### Top-down
``` java
import java.util.*;
import java.io.*;

class Main {
    static int T, N, M;
    static int[][] board, dp;

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        T = Integer.parseInt(st.nextToken());

        for (int test = 0; test < T; test++) {
            st = new StringTokenizer(br.readLine(), " ");
            N = Integer.parseInt(st.nextToken());
            M = Integer.parseInt(st.nextToken());

            board = new int[N][M];
            dp = new int[N][M];

            for (int j = 0; j < N; j++) {
                for (int i = 0; i < M; i++) {
                    dp[j][i] = -1;
                }
            }

            st = new StringTokenizer(br.readLine(), " ");
            for (int j = 0; j < N; j++) {
                for (int i = 0; i < M; i++) {
                    board[j][i] = Integer.parseInt(st.nextToken());
                }
            }

            int ans = Integer.MIN_VALUE;

            for (int j = 0; j < N; j++) {
                ans = Math.max(ans, dfs(j, 0));
            }

            bw.write(ans + "\n");
        }

        bw.flush();
    }

    private static int dfs(int y, int x) {
        if (x == M - 1) {
            return board[y][x];
        }

        if (dp[y][x] != -1) return dp[y][x];

        int max = Integer.MIN_VALUE;
        for (int j = -1; j <= 1; j++) {
            if (isValid(y + j)) max = Math.max(max, dfs(y + j, x + 1) + board[y][x]);
        }

        return dp[y][x] = max;
    }

    private static boolean isValid(int y) {
        return 0 <= y && y <= N - 1;
    }
}
```
