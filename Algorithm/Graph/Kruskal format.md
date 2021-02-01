``` java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); // node 개수
        int m = sc.nextInt(); // edge 개수

        int[] parent = new int[n + 1];

        for (int i = 0; i <= parent.length; i++) {
            parent[i] = i;
        }

        PriorityQueue<Edge> pq = new PriorityQueue<>((e1, e2) -> e1.distance - e2.distance);

        for (int i = 0; i < m; i++) {
            int nodeA = sc.nextInt();
            int nodeB = sc.nextInt();
            int distance = sc.nextInt();

            pq.offer(new Edge(nodeA, nodeB, distance));
        }

        while (!pq.isEmpty()) {
            Edge edge = pq.poll();
            
            union(parent, edge.node[0], edge.node[1]);
        }
    }

    private static int getParent(int[] parent, int a) {
        if (a == parent[a]) return a;

        return parent[a] = getParent(parent, parent[a]);
    }

    private static void union(int[] parent, int a, int b) {
        a = getParent(parent, a);
        b = getParent(parent, b);

        if (a == b) return; // 부모의 값이 같은 경우에는 skip (사이클 형성)

        if (a < b) {
            parent[b] = a;
        } else {
            parent[a] = b;
        }
    }

    static class Edge{
        int[] node;
        int distance;

        Edge(int nodeA, int nodeB, int distance) {
            node = new int[2];
            node[0] = nodeA;
            node[1] = nodeB;

            this.distance = distance;
        }
    }
}
```

- 최소 길이를 기준으로 edge 정렬  
- 부모 노드가 동일한 경우에는 cycle이 형성되었기에 제외  
