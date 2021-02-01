```java 
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        if (numCourses == 0) return new int[]{};
        
        int index = 0;
        int[] order = new int[numCourses];
        int[] indegree = new int[numCourses];
        boolean[] visited = new boolean[numCourses];
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        Queue<Integer> queue = new LinkedList<>();
        
        for (int i=0; i<numCourses; i++) {
            adjList.add(new ArrayList<Integer>());
        }
        
        for (int[] course : prerequisites) {
            indegree[course[0]]++;
            adjList.get(course[1]).add(course[0]);
        }
        
        for (int i=0; i<numCourses; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
            }
        }
        
        while (!queue.isEmpty()) {
            int course = queue.poll();
            visited[course] = true;
            order[index] = course;
            index = index+1;
            
            for (int c : adjList.get(course)) {
                indegree[c]--;
                if (!visited[c] && indegree[c] == 0) {
                    queue.offer(c);
                }
            }
        }
        
        return (index == numCourses) ? order : new int[]{};
    }
}
``` 

#### 확인
1. 예외 처리
2. empty array return시 new int[]{}
3. boolean[] visited
4. topological sort 완성 가능 여부는 index가 끝값에 도달해야. 0이 아닌 경우로 판단하면 
