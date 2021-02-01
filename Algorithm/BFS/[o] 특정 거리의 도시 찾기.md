``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        boolean[] visited;
        Queue<Integer> queue = new LinkedList<>();
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        ArrayList<Integer> targetCity = new ArrayList<>();

        int dist = -1;

        st = new StringTokenizer(br.readLine(), " ");

        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());
        int X = Integer.parseInt(st.nextToken());

        visited = new boolean[N+1];

        for (int i = 0; i <= N; i++) {
            adjList.add(new ArrayList<>());
        }
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine(), " ");

            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());

            adjList.get(from).add(to);
        }

        queue.offer(X);
        while (!queue.isEmpty()) {
            dist = dist + 1;
            int size = queue.size();

            for (int k = 0; k < size; k++) {
                int city = queue.poll();

                for (int adj : adjList.get(city)) {
                    if (!visited[adj]) {
                        visited[adj] = true;
                        queue.offer(adj);
                    }
                }

                if (dist == K) targetCity.add(city);
            }
        }

        Collections.sort(targetCity);

        if (targetCity.size() == 0) {
            bw.write(-1 + "\n");
        } else {
            for (int i = 0; i < targetCity.size(); i++) {
                bw.write(targetCity.get(i) + "\n");
            }
        }

        bw.flush();

        br.close();
        bw.close();
    }
}
```
