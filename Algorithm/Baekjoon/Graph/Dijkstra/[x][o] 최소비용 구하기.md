```java
import java.io.*;
import java.util.*;

class Main {
    static int N, M;
    static int[] cost;
    static boolean[] check;
    static ArrayList<ArrayList<Node>> adjList = new ArrayList<>();

    public static void main(String args[]) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        N = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());

        cost = new int[N+1];
        check = new boolean[N+1];

        Arrays.fill(cost, Integer.MAX_VALUE);
        for (int i=0; i<N+1; i++) {
            adjList.add(new ArrayList<>());
        }

        for (int i=1; i<=M; i++) {
            st = new StringTokenizer(br.readLine(), " ");

            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            adjList.get(from).add(new Node(to, c));
        }

        st = new StringTokenizer(br.readLine(), " ");

        int start = Integer.parseInt(st.nextToken());
        int end = Integer.parseInt(st.nextToken());
        cost[start] = 0;

        bw.write(dijkstra(start, end) + "\n");
        bw.flush();
        br.close();
        bw.close();
    }

    static int dijkstra(int start, int end) {
        PriorityQueue<Node> pq = new PriorityQueue<>();

        pq.offer(new Node(start, cost[start]));
        while (!pq.isEmpty()) {
            Node node = pq.poll();
            if (!check[node.end]) {
                check[node.end] = true;

                for (Node n : adjList.get(node.end)) {
                    if (!check[n.end] && cost[n.end] > cost[node.end] + n.cost) {
                        cost[n.end] = cost[node.end] + n.cost;
                        pq.offer(new Node(n.end, cost[n.end]));
                    }
                }
            }
        }

        return cost[end];
    }

    static class Node implements Comparable<Node> {
        int end;
        int cost;

        Node(int end, int cost) {
            this.end = end;
            this.cost = cost;
        }

        @Override
        public int compareTo(Node o) {
            return (this.cost - o.cost > 0) ? 1 : -1;
        }
    }
}
```

#### 확인
1. priorityQueue에 Comparable 인터페이스를 구현할 때는 오름차순으로 정렬을 하면 최소값이 출력된다.  
기본이 최소값이라고 생각하면 될 듯 하다.
