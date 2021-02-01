각 index별로 min,max 계산이 필요. 가로는 3 세로는 1<=N<=100000   
하지만 메모리가 4MB  

#### Bottom-up
현재 y에 대한 계산을 위해서 y-1의 결과값만 필요하다는걸 생각하면 모든 y에 대한 dp를 생성할 필요가 없다  
또한 입력값 또한 배열에 저장할 필요가 없다  

```java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        int N = Integer.parseInt(st.nextToken());

        Node[][] dp = new Node[2][3];
        for (int j=0; j<2; j++) {
            for (int i=0; i<3; i++) {
                dp[j][i] = new Node(0, 0);
            }
        }

        for (int j=0; j<N; j++) {
            st = new StringTokenizer(br.readLine(), " ");

            int indexResult = (j%2 == 0) ? 0 : 1;
            int indexCalc = (j%2 == 0) ? 1 :0;

            for (int i=0; i<3; i++) {
                int num = Integer.parseInt(st.nextToken());
                int min = Integer.MAX_VALUE;
                int max = Integer.MIN_VALUE;

                for (int k=-1; k<=1; k++) {
                    int indexX = i+k;

                    if (0 <= indexX && indexX < 3) {
                        min = Math.min(min, dp[indexCalc][indexX].min + num);
                        max = Math.max(max, dp[indexCalc][indexX].max + num);
                    }
                }

                dp[indexResult][i].min = min;
                dp[indexResult][i].max = max;
            }
        }

        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        int indexAnswer = ((N-1) % 2 == 0) ? 0 : 1;

        for (int i=0; i<3; i++) {
            Node node = dp[indexAnswer][i];
            min = Math.min(min, node.min);
            max = Math.max(max, node.max);
        }

        bw.write(max + " " + min);
        bw.flush();
        br.close();
        bw.close();
    }

    static class Node {
        int min, max;

        Node(int min, int max) {
            this.min = min;
            this.max = max;
        }
    }
}
```

#### Top-down (메모리 초과)
```java
import java.util.*;
import java.io.*;

class Main {
    static int len;
    static Node[][] dp;
    static int[][] nums;

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        len = Integer.parseInt(st.nextToken());

        dp = new Node[len][len];
        nums = new int[len][len];

        for (int j=0; j<len; j++) {
            st = new StringTokenizer(br.readLine(), " ");
            for (int i=0; i<len; i++) {
                nums[j][i] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i=0; i<len; i++) {
            findMinMax(0, i);
        }

        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        for (int i=0; i<len; i++) {
            Node node = dp[0][i];
            min = Math.min(node.min, min);
            max = Math.max(node.max, max);
        }

        bw.write(max + " " + min);
        bw.flush();
    }

    private static Node findMinMax(int j, int i) {
        if (j == len-1) {
            return new Node(nums[j][i], nums[j][i]);
        }

        if (dp[j][i] != null) {
            return dp[j][i];
        }

        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;

        for (int k=-1; k<=1; k++) {
            int index = i+k;
            if (0 <= index && index <= len-1) {
                Node node = findMinMax(j+1, index);
                min = Math.min(min, nums[j][i] + node.min);
                max = Math.max(max, nums[j][i] + node.max);
            }
        }

        dp[j][i] = new Node(min, max);
        return dp[j][i];
    }

    static class Node {
        int min, max;

        Node(int min, int max) {
            this.min = min;
            this.max = max;
        }
    }
}
```

#### 확인
1. 메모리 제약사항 
