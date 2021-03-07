1. 간선 데이터를 비용에 따라 오름차순으로 정렬  
2. 간선을 하나씩 확인하며 사이클 발생시키는지 확인 (발생하지 않는 경우에만 최소 신장 트리에 포함)  
3. 모든 간선에 대하여 2번 과정 반복 

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


``` py 
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)

    if a < b:
        parent[b] = a
    else:
        parent[a] = b


v, e = map(int, input().split())
parent = [0] * (v + 1)
edges = []
result = 0

for i in range(1, v + 1):
    parent[i] = i

for _ in range(e):
    a, b, cost = map(int, input().split())
    edges.append((cost, a, b))

edges.sort()

for edge in edges:
    cost, a, b = edge

    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost
```
