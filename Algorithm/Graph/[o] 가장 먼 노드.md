```java  
import java.util.*;

class Solution {
    public int solution(int n, int[][] edge) {        
        int count = 0;
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        boolean[] visited = new boolean[n+1];
        Queue<Integer> queue = new LinkedList<>();
        
        for (int i=0; i<=n; i++) {
            adjList.add(new ArrayList<Integer>());
        }
        
        for (int[] e : edge) {
            adjList.get(e[0]).add(e[1]);
            adjList.get(e[1]).add(e[0]);            
        }
        
        queue.offer(1);        
        visited[1] = true;
        while (!queue.isEmpty()) {
            int size = queue.size();                        
            
            for (int i=0; i<size; i++) {                
                int node = queue.poll();                                
                for (int neighbor : adjList.get(node)) {
                    if (!visited[neighbor]) {
                        visited[neighbor] = true;
                        queue.offer(neighbor);                        
                    }
                }
            }            
            count = size;
        }
        
        return count;
    }
}
```
