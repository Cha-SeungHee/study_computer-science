``` java
import java.util.*;
import java.io.*;

class Main {
    static int N;
    static int[] dp;
    static int[] primeFactor = {2, 3, 5};

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        N = Integer.parseInt(br.readLine());
        dp = new int[5001];

        Arrays.fill(dp, 0);

        dp[1] = 1;

        for (int i = 1; i <= 1000; i++) {
            for (int k = 0; k < 3; k++) {
                dp[i * primeFactor[k]] = dp[i] + 1;
            }
        }

        int count = 0;
        int ans = 0;
        for (int i = 1; i <= 5000; i++) {
            if (dp[i] > 0) {
                count = count + 1;

                if (count == N) {
                    ans = i;
                    break;
                }
            }
        }

        bw.write(ans +  "\n");
        bw.flush();

        br.close();
        bw.close();
    }
}
```
