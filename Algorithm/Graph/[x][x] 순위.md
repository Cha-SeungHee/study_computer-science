```java  
import java.util.*;

class Solution {
    public int solution(int n, int[][] results) {        
        ArrayList<ArrayList<Integer>> adjListWinner = new ArrayList<>();
        ArrayList<ArrayList<Integer>> adjListLoser = new ArrayList<>();
        
        for (int i=0; i<=n; i++) {
            adjListWinner.add(new ArrayList<>());
            adjListLoser.add(new ArrayList<>());
        }
        
        for (int[] result : results) {
            adjListWinner.get(result[1]).add(result[0]);
            adjListLoser.get(result[0]).add(result[1]);
        }
        
        int cnt = 0;
        for (int i=1; i<=n; i++) {
            cnt = cnt + helper(i, n, adjListWinner, adjListLoser);
        }
        
        return cnt;
    }
    
    private int helper(int player, int n, ArrayList<ArrayList<Integer>> adjListWinner, ArrayList<ArrayList<Integer>> adjListLoser) {
        int winner = countHelper(player, n, adjListWinner);
        int loser = countHelper(player, n, adjListLoser);        
        
        return (winner + loser == n+1) ? 1 : 0;
    }
    
    private int countHelper(int player, int n, ArrayList<ArrayList<Integer>> adjList) {
        Queue<Integer> queue = new LinkedList<>();
        boolean[] visited = new boolean[n+1];
        queue.offer(player);
        visited[player] = true;
        int count = 0;
        while (!queue.isEmpty()) {
            int node = queue.poll();
            count = count+1;
            for (int p : adjList.get(node)) {
                if (!visited[p]) {
                    visited[p] = true;
                    queue.offer(p);
                }
            }
        }
        return count; 
    }
}
``` 

#### 확인
1. 순위를 매길 수 있는 선수의 조건을 생각하지 못함

2. 조건을 생각했을 때는 각 선수에 대해 bfs를 다 돌려본다는 생각을 하지 못함 (항상 입력값 범위를 확인 후 시간 복잡도로 먼저 추측할 수 있어야 한다)  
