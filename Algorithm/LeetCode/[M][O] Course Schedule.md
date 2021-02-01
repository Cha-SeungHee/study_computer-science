``` java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (prerequisites == null || prerequisites.length == 0) return true;
        
        int take = 0;
        int[] indegree = new int[numCourses];
        
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        
        for (int i = 0; i < numCourses; i++) {
            adjList.add(new ArrayList<>());
        }
        
        for (int[] pre : prerequisites) {
            adjList.get(pre[1]).add(pre[0]);
            indegree[pre[0]]++;
        }
        
        Queue<Integer> queue = new LinkedList<>();
        
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) queue.offer(i);
        }
        
        while (!queue.isEmpty()) {
            int course = queue.poll();
            take = take + 1;
            
            for (int post : adjList.get(course)) {
                indegree[post] = indegree[post] - 1;
                
                if (indegree[post] == 0) {
                    queue.offer(post);                    
                }
            }            
        }
        
        return take == numCourses;
    }
}
```
