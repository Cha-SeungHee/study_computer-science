```` java
import java.util.*;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        Queue<Task> queue = new LinkedList<>();
        ArrayList<Integer> completeCountList = new ArrayList<>();
        
        for (int i = 0; i < progresses.length; i++) {
            queue.offer(new Task(progresses[i], speeds[i]));
        }
        
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            int count = 0;
            
            Task task = queue.peek();
            if (task.progress >= 100) {
                while (!queue.isEmpty() && queue.peek().progress >= 100) {
                    queue.poll();
                    count = count + 1;
                }
            } else {
                for (int k = 0; k < size; k++) {
                    Task temp = queue.poll();
                    queue.offer(new Task(temp.progress + temp.speed, temp.speed));
                }
            }
            
            if (count > 0) completeCountList.add(count);
        }
        
        int[] answer = new int[completeCountList.size()];
        for (int i = 0; i < completeCountList.size(); i++) {
            answer[i] = completeCountList.get(i);
        }        
        
        return answer;
    }
}

class Task {
    int progress;
    int speed;
    int index;
    
    Task(int progress, int speed) {
        this.progress = progress;
        this.speed = speed;
    }
}
````
