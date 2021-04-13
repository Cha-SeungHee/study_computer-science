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

``` py
from collections import deque

class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        inorder = [0] * numCourses
        visited = [False] * numCourses
        adjList = [[] for i in range(numCourses)]
        numCourse = 0
        
        for pre in prerequisites:
            after, before = pre[0], pre[1]
            adjList[before].append(after)
            inorder[after] += 1
        
        queue = deque()    
        for index, value in enumerate(inorder):
            if value == 0:
                queue.append(index)
                visited[index] = True
        
        while queue:
            course = queue.pop()                 
            numCourse += 1
            
            for nextCourse in adjList[course]:
                inorder[nextCourse] -= 1
                
                if not visited[nextCourse] and inorder[nextCourse] == 0:
                    queue.append(nextCourse)
                    visited[nextCourse] = True
        
        return numCourse == numCourses
```
