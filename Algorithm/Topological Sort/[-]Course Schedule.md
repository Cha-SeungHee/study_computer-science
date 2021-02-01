```java 
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (prerequisites == null || prerequisites.length == 0) return true;
        
        int courseTaken = 0;
        int[] indegree = new int[numCourses];
        boolean[] visited = new boolean[numCourses];
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();        
        Queue<Integer> q = new LinkedList<>();
        
        for (int i=0; i<numCourses; i++) {
            adjList.add(new ArrayList<Integer>());
        }        
        
        for (int[] pre : prerequisites) {
            indegree[pre[0]]++;
            adjList.get(pre[1]).add(pre[0]);            
        }        
        
        for (int i=0; i<numCourses; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
            }
        }
        
        while (!q.isEmpty()) {
            int course = q.poll();            
            courseTaken++;
            visited[course] = true;
            for (int c : adjList.get(course)) {
                if (!visited[c]) {
                    indegree[c]--;
                    if (indegree[c] == 0) {
                        q.offer(c);
                    }
                }
            }
        }
        
        return courseTaken == numCourses;
    }
}
```java 

#### 확인
1. visited 놓침
2. adjList 순서를 잘 생각해야함
3. 
indegree[i] : i는 prerequisite x
adjList.get(i).add(j) : i는 prerequisite 
4. index가 0번에서 시작하는지 1번에서 시작하는지 확인하는 것도 중요
