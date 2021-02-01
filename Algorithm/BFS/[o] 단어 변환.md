```` java
import java.util.*;

class Solution {
    public int solution(String begin, String target, String[] words) {        
        int count = 0;        
        Queue<String> queue = new LinkedList<>();
        HashMap<String, Boolean> visited = new HashMap<>();
        
        for (String word : words) {
            visited.put(word, false);
        }            
        
        queue.offer(begin);
        visited.put(begin, true);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            count = count + 1;
            
            for (int k = 0; k < size; k++) {
                String current = queue.poll();    
                
                if (current.equals(target)) return count - 1;
                
                for (String word : words) {
                    if (current.equals(word)) continue;
                    if (!visited.get(word) && isValid(current, word)) {
                        visited.put(word, true);
                        queue.offer(word);
                    }   
                }
            }
        }        
        
        return 0;
    }
    
    private boolean isValid(String word1, String word2) {
        int count = 0;
        
        for (int i = 0; i < word1.length(); i++) {
            if (word1.charAt(i) != word2.charAt(i)) {
                count = count + 1;
            }            
            if (count > 1) {                
                break;
            }            
        }
        
        return count == 1;
    }
}
````
