기본적으로 Sliding Window 문제는 O(n)으로 풀어야 한다

#### 개선한 코드
Deque에 앞을 최소값, 뒤를 최대값으로 매번 삽입 (새로 삽입될 값에 비해 더 큰 뒤에 있는 값들은 삭제한 뒤 삽입   

```java  
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        Deque<Node> dq = new LinkedList<>();

        st = new StringTokenizer(br.readLine(), " ");
        int N = Integer.parseInt(st.nextToken());
        int L = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine(), " ");
        for (int i=0; i<N; i++) {
            int num = Integer.parseInt(st.nextToken());

            while (!dq.isEmpty() && dq.getLast().num > num) {
                dq.removeLast();
            }
            dq.addLast(new Node(num, i));
            if (dq.getFirst().index <= i-L) {
                dq.removeFirst();
            }
            bw.write(dq.getFirst().num + " ");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    static class Node {
        int num;
        int index;

        Node (int num, int index) {
            this.num = num;
            this.index = index;
        }
    }
}
```

#### 시간 초과 코드
하나씩 이동하면서 최소값을 찾기 위해 PriorityQueue를 사용했음  
PriorityQueue 자체에 정렬을 위한 시간이 필요하므로 시간 초과 발생  

```java  
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int[] nums;
        HashMap<Integer, Integer> map = new HashMap<>();
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        st = new StringTokenizer(br.readLine(), " ");
        int N = Integer.parseInt(st.nextToken());
        int L = Integer.parseInt(st.nextToken());

        nums = new int[N];

        st = new StringTokenizer(br.readLine(), " ");
        for (int i=0; i<N; i++) {
            nums[i] = Integer.parseInt(st.nextToken());
        }

        int end = 0, start = end-L+1;

        while (end < N) {
            int min = Integer.MAX_VALUE;

            if (map.containsKey(nums[end])) {
                map.put(nums[end], map.get(nums[end])+1);
            } else {
                map.put(nums[end], 1);
            }

            if (map.get(nums[end]) == 1) {
                pq.offer(nums[end]);
            }

            if (!pq.isEmpty()) min = Math.min(min, pq.peek());

            if (start >= 0) {
                if (map.containsKey(nums[start])) {
                    map.put(nums[start], Math.max(map.get(nums[start]) - 1, 0));
                }
                if (map.get(nums[start]) == 0) {
                    pq.remove(nums[start]);
                }
            }

            end = end+1;
            start = start+1;

            bw.write(min + " ");
        }

        bw.write("\n");
        bw.flush();
        bw.close();
        br.close();
    }
}
```
