```java
import java.io.*;
import java.util.*;

class Main {
    public static void main(String args[]) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int numPC = Integer.parseInt(br.readLine());
        int branch = Integer.parseInt(br.readLine());

        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        for (int i=0; i<=numPC; i++) {
            adjList.add(new ArrayList<>());
        }

        for (int i=0; i<branch; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());

            adjList.get(from).add(to);
            adjList.get(to).add(from);
        }

        int count = 0;
        boolean[] visited = new boolean[numPC+1];

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(1);
        visited[1] = true;
        while (!queue.isEmpty()) {
            int pc = queue.poll();            
            count = count+1;
            for (int connected : adjList.get(pc)) {
                if (!visited[connected]) {
                    visited[connected] = true;
                    queue.offer(connected);
                }
            }
        }

        System.out.println(count-1);
    }
}
```
