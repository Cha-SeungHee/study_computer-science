```java
import java.io.*;
import java.util.*;

class Main {
    static int V, E, start;
    static int[] cost;
    static boolean[] check;
    static ArrayList<ArrayList<Node>> adjList;

    public static void main(String args[]) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine(), " ");
        start = Integer.parseInt(st.nextToken());

        cost = new int[V+1];
        check = new boolean[V+1];
        adjList = new ArrayList<>();

        Arrays.fill(cost, Integer.MAX_VALUE);
        for (int i=0; i<=V; i++) {
            adjList.add(new ArrayList<>());
        }

        for (int i=1; i<=E; i++) {
            st = new StringTokenizer(br.readLine(), " ");

            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            adjList.get(from).add(new Node(to, c));
        }

        for (int i=1; i<=V; i++) {
            int result = dijkstra(start, i);
            String resultString = (result == Integer.MAX_VALUE) ? "INF" : Integer.toString(result);
            bw.write(resultString + "\n");
        }
        bw.flush();
        br.close();
        bw.close();
    }

    private static int dijkstra(int start, int end) {
        PriorityQueue<Node> pq = new PriorityQueue<>();

        cost[start] = 0;

        pq.offer(new Node(start, cost[start]));
        while(!pq.isEmpty()) {
            Node node = pq.poll();
            if (!check[node.id]) {
                check[node.id] = true;

                for (Node n : adjList.get(node.id)) {
                    if (cost[n.id] > cost[node.id] + n.cost) {
                        cost[n.id] = cost[node.id] + n.cost;
                        pq.offer(new Node(n.id, cost[n.id]));
                    }
                }
            }
        }

        return cost[end];
    }

    static class Node implements Comparable<Node> {
        int id;
        int cost;

        Node(int id, int cost) {
            this.id = id;
            this.cost = cost;
        }

        @Override
        public int compareTo(Node o) {
            return (cost - o.cost) > 0 ? 1 : -1;
        }
    }
}
```
