``` java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        if (numCourses == 0) return new int[]{};
        
        int[] course = new int[numCourses];
        
        int[] indegree = new int[numCourses];
        ArrayList<Integer> courseList = new ArrayList<>();
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
            int courseTaken = queue.poll();
            courseList.add(courseTaken);
            
            for (int c : adjList.get(courseTaken)) {
                indegree[c] = indegree[c] - 1;
                
                if (indegree[c] == 0) {
                    queue.offer(c);
                }
            }            
        }
        
        if (courseList.size() != numCourses) return new int[]{};
        
        for (int i = 0; i < courseList.size(); i++) {
            course[i] = courseList.get(i);
        }
        
        return course;
    }
}
```

- 예외 처리 (numCourse 0일 때 처리 / prerequisites 크기 0 또는 null 일 때 별도의 예외 처리 없어도 로직 내에서 해결)
- Empty array return -> new int[]{}  
