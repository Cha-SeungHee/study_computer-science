``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        int N;

        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        ArrayList<Integer> list = new ArrayList<>();

        N = Integer.parseInt(br.readLine());

        st = new StringTokenizer(br.readLine(), " ");
        for (int i = 0; i < N; i++) {
            list.add(Integer.parseInt(st.nextToken()));
        }

        Collections.sort(list);

        bw.write(list.get((N-1)/2) + "\n");
        bw.flush();
    }
}
```
