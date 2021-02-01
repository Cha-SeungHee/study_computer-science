```java  
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int N = 0, sumPart = 0;
        long sum = 0;
        String word = null;

        st = new StringTokenizer(br.readLine(), " ");

        N = Integer.parseInt(st.nextToken());
        word = br.readLine();

        for (int i=0; i<N; i++) {
            char ch = word.charAt(i);
            if (isNumber(ch)) {
                sumPart = sumPart*10 + ch-'0';
            } else {
                sum = sum+sumPart;
                sumPart = 0;
            }
        }
        if (sumPart > 0) {
            sum += sumPart;
        }

        bw.write(sum + "\n");
        bw.flush();

        br.close();
        bw.close();
    }

    private static boolean isNumber(char ch) {
        return '0' <= ch && ch <= '9';
    }
}
```
