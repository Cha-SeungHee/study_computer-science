```` java
import java.util.*;

class Solution {
    public int solution(int[] priorities, int location) {
        int order = 1;
        ArrayList<Document> list = new ArrayList<>();
        Queue<Document> queue = new LinkedList<>();
        PriorityQueue<Document> pq = new PriorityQueue<>();
        
        for (int i = 0; i < priorities.length; i++) {
            Document document = new Document(i, priorities[i]);
            
            list.add(document);
            queue.offer(document);
            pq.offer(document);
        }
        
        while (!queue.isEmpty()) {
            Document document = queue.poll();
            
            if (document.priority >= pq.peek().priority) {
                document.order = order;                
                order = order + 1;                
                pq.poll();
            } else {
                queue.offer(document);
            }
        }
        
        return list.get(location).order;
    }
}

class Document implements Comparable<Document> {
    int index;
    int priority;
    int order = 0;
    
    Document(int index, int priority) {
        this.index = index;
        this.priority = priority;
    }
    
    @Override
    public int compareTo(Document o) {
        return (this.priority > o.priority) ? -1 : (this.priority < o.priority) ? 1 : 0;
    }
}
````
