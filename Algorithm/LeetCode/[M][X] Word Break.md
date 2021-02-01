``` java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if (s == null || s.length() == 0) return true;
        
        boolean added = true;        
        Queue<String> queue = new LinkedList<>();
        Set<String> set = new HashSet<>();
        StringBuilder sb;
        queue.offer("");        
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            
            for (int k = 0; k < size; k++) {
                String string = queue.poll();
                
                if (string.equals(s)) return true;
                
                if (string.length() >= s.length()) continue;
                
                for (String option : wordDict) {
                    int begin = string.length();
                    int end = string.length() + option.length();
                    
                    if (end > s.length()) continue;
                    
                    String temp = s.substring(begin, end);
                    
                    if (option.equals(temp)) {
                        sb = new StringBuilder();
                        sb.append(string);
                        sb.append(option);
                        
                        if (set.add(sb.toString())) queue.offer(sb.toString());
                    }
                }
            }            
        }
        
        return false;
    }
}
``` 

Dictionary에 있는 단어 목록으로 s를 만들 수 있는지 확인하는 문제  
- BFS로 시도하되, queue에 삽입하는 조건은 dictionary에 있는 단어와 string의 이번 index 구간의 string이 동일한지 확인하는 부분  
- 또한 반복적인 연산을 막기 위해 HashSet<String>을 사용  
