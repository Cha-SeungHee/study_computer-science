``` java
import java.util.*;
import java.io.*;

class Main {
    static int[][] board;
    static int[][] dp;

    static int N;

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());

        board = new int[N][N];
        dp = new int[N][N];

        for (int j = 0; j < N; j++) {
            st = new StringTokenizer(br.readLine(), " ");

            for (int i = 0; i <= j; i++) {
                board[j][i] = Integer.parseInt(st.nextToken());
            }
        }

        dp[0][0] = board[0][0];

        for (int j = 0; j < N - 1; j++) {
            for (int i = 0; i <= j; i++) {
                dp[j + 1][i] = Math.max(dp[j + 1][i], dp[j][i] + board[j + 1][i]);
                dp[j + 1][i + 1] = Math.max(dp[j + 1][i + 1], dp[j][i] + board[j + 1][i + 1]);
            }
        }

        int max = Integer.MIN_VALUE;
        for (int i = 0; i < N; i++) {
            max = Math.max(max, dp[N - 1][i]);
        }

        bw.write(max + "\n");
        bw.flush();

        br.close();
        bw.close();
    }
}
```
