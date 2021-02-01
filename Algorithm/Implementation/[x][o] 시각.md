``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer(br.readLine(), " ");

        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        int count = 0;

        for (int hh = 0; hh <= N; hh++) {
            for (int mm = 0; mm <= 59; mm++) {
                for (int ss = 0; ss<= 59; ss++) {
                    if (check(hh, mm, ss, K)) count = count + 1;
                }
            }
        }

        bw.write(count + "\n");
        bw.flush();
    }

    static boolean check(int h, int m, int s, int K) {
        return (h / 10 == K || h % 10 == K || m / 10 == K || m % 10 == K || s / 10 == K || s % 10 == K);
    }
}
```

#### 확인
1. 시간 관련 계산할 때 3중 for 문 사용하면 편하구나  
2. 시간, 분, 초에 대해 3이 있는지 각각 계산하면 된다. 굳이 하나로 합칠 필요가 없다  
