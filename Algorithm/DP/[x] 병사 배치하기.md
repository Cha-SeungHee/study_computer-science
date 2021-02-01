#### Longest Decreasing Subsequence

``` java
import java.util.*;
import java.io.*;

class Main {
    static int N;
    static int[] nums;
    static int[] dp;

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        N = Integer.parseInt(br.readLine());
        nums = new int[N];
        dp = new int[N];

        st = new StringTokenizer(br.readLine(), " ");
        for (int i = 0; i < N; i++) {
            nums[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.fill(dp, 1);

        for (int i = 1; i < N; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] > nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }

        int longest = 0;
        for (int i = 0; i < N; i++) {
            longest = Math.max(longest, dp[i]);
        }


        bw.write(N - longest +  "\n");
        bw.flush();

        br.close();
        bw.close();
    }
}
```
