#### 빈도수 우선 Queue
빈도수가 가장 높은 수를 반환하는 Queue 만들기  
빈도수가 동일하다면 가장 먼저 enqueue된 수를 반환하고 제거
FQ가 비어있으면 -1을 반환  

```java 
import java.util.*;
import java.io.*;

class Main {
    static HashMap<Integer, Integer> map;
    static PriorityQueue<Node> pq;
    static int count = 0;
    static BufferedReader br;
    static BufferedWriter bw;

    public static void main(String[] args) throws IOException{
        StringTokenizer st;
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));

        map = new HashMap<>();
        pq = new PriorityQueue<>();

        st = new StringTokenizer(br.readLine(), " ");
        int numLine = Integer.parseInt(st.nextToken());


        for (int i=0; i<numLine; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            String command  = st.nextToken();
            if (command.equals("enqueue")) {
                int num = Integer.parseInt(st.nextToken());
                enqueue(num);
            } else {
                dequeue();
            }
        }

        bw.flush();
        br.close();
        bw.close();
    }

    private static void enqueue(int num) {
        if (map.containsKey(num)) {
            map.put(num, map.get(num)+1);

            PriorityQueue<Node> pqTmp = new PriorityQueue<>();
            while (!pq.isEmpty()) {
                Node nodeTmp = pq.poll();
                pqTmp.offer(new Node(nodeTmp.num, nodeTmp.order));
            }

            pq = pqTmp;
        } else {
            map.put(num, 1);
        }

        pq.offer(new Node(num, count));
        count = count+1;
    }

    private static void dequeue() throws IOException {
        if (!pq.isEmpty()) {
            Node node = pq.poll();
            bw.write(node.num + " ");

            if (map.get(node.num) > 1) {
                map.put(node.num, map.get(node.num)-1);

                PriorityQueue<Node> pqTmp = new PriorityQueue<>();
                while (!pq.isEmpty()) {
                    Node nodeTmp = pq.poll();

                    pqTmp.offer(new Node(nodeTmp.num, nodeTmp.order));
                }

                pq = pqTmp;
            }
        } else {
            bw.write(-1 + " ");
        }
    }

    static class Node implements Comparable<Node>{
        int num;
        int order;

        Node (int num, int order) {
            this.num = num;
            this.order = order;
        }

        @Override
        public int compareTo(Node o) {
            return (map.get(num) > map.get(o.num)) ? -1 : (map.get(num) < map.get(o.num)) ? 1 : (order > o.order) ? 1 : -1;
        }
    }
}
```

#### 확인
1. PriorityQueue의 정렬순서 (기본기 문제)  
2. Enqueue 및 Dequeue 일 때 모두 정렬 기준(개수 : map.get(num))이 변하기 때문에 새로 정렬을 해줘야 한다  
3. 더 효율적인 알고리즘은 뭐가 있을까? 현재는 enqueue/dequeue 각각 O(nlogn)            
