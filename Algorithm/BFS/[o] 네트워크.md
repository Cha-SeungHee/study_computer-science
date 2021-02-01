```` java
import java.util.*;

class Solution {
    boolean[] visited;
    ArrayList<ArrayList<Integer>> adjList;
    
    public int solution(int n, int[][] computers) {
        int count = 0;

        visited = new boolean[n];
        adjList = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            adjList.add(new ArrayList<Integer>());
        }

        for (int[] network : computers) {
            for (int i = 0; i < network.length; i++) {
                if (network[i] == 1) {
                    for (int j = i + 1; j < network.length; j++) {
                        if (network[j] == 1) {
                            ArrayList<Integer> sublist = adjList.get(i);
                            if (!sublist.contains(j)) sublist.add(j);

                            sublist = adjList.get(j);
                            if (!sublist.contains(i)) sublist.add(i);
                        }
                    }
                }
            }
        }

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                bfs(i);
                count = count + 1;
            }
        }
        
        return count;
    }
    
    public void bfs(int start) {
        Queue<Integer> queue = new LinkedList<>();
        visited[start] = true;

        queue.offer(start);

        while (!queue.isEmpty()) {
            int node = queue.poll();

            for (int adj : adjList.get(node)) {
                if (!visited[adj]) {
                    queue.offer(adj);
                    visited[adj] = true;
                }
            }
        }
    }
}
````
