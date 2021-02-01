``` java
class Solution {
    public int minReorder(int n, int[][] connections) {
        int countReverse = 0;
        
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        HashMap<Integer, ArrayList<Integer>> map = new HashMap<>();
        boolean[] visited = new boolean[n];
        
        for (int i = 0; i < n; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] pair : connections) {
            adjList.get(pair[0]).add(pair[1]);
            
            if (map.get(pair[0]) == null) map.put(pair[0], new ArrayList<>());
            map.get(pair[0]).add(pair[1]);
            
            adjList.get(pair[1]).add(pair[0]);
        }
        
        Queue<Integer> queue = new LinkedList<>();
        
        queue.offer(0);
        visited[0] = true;        
                
        while (!queue.isEmpty()) {
            int num = queue.poll();
            
            for (int adjNum : adjList.get(num)) {
                boolean right = false;
                
                if (visited[adjNum]) continue;               
                
                if (!isInDirection(map, adjNum, num)) {                    
                    countReverse = countReverse + 1;
                }
                
                visited[adjNum] = true;
                queue.offer(adjNum);
            }
        }
            
        return countReverse;        
    }
    
    private boolean isInDirection(HashMap<Integer, ArrayList<Integer>> map, int num, int target) {
        if (!map.containsKey(num)) return false;
        
        boolean right = false;
        
        for (int node : map.get(num)) {
            if (node == target) {
                right = true;
                break;
            }
        }
        
        return right;
    }
}
```

- "From to To" 정보를 담는 HashSet을 사용하여 0으로 가기 위한 "From to To" 정보가 HashSet에 존재한는걸 파악했다면 isInDirection 함수를 사용할 필요가 없음  
