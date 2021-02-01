```` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int numTest = Integer.parseInt(br.readLine());

        for (int testCase = 0; testCase < numTest; testCase++) {
            st = new StringTokenizer(br.readLine(), " ");
            int H = Integer.parseInt(st.nextToken());
            int W = Integer.parseInt(st.nextToken());
            int order = Integer.parseInt(st.nextToken());

            int room = order / H + 1;
            int floor = order % H;

            if (floor == 0) {
                floor = H;
                room = room -1;
            }

            int ans = floor * 100 + room;

            bw.write(ans + "\n");
        }

        bw.flush();
    }
}
````
