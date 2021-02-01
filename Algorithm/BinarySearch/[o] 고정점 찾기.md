``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws Exception {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int N = Integer.parseInt(br.readLine());
        int[] arr = new int[N];

        st = new StringTokenizer(br.readLine(), " ");
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        bw.write(binarySerach(arr) + "\n");
        bw.flush();

        bw.close();
    }

    private static int binarySerach(int[] arr) {
        int start = 0;
        int end = arr.length - 1;

        while (start < end) {
            int mid = start + (end - start) / 2;

            if (arr[mid] == mid) return mid;

            if (arr[mid] > mid) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }

        return (arr[start] == start) ? start : -1;
    }
}
```
