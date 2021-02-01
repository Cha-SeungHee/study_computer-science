포맷에 맞춘 

```java  
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
        
        HashMap<Character, Integer> map = new HashMap<>();
        int start = 0, end = 0, condition = 0, max = Integer.MIN_VALUE;
        
        while (end < s.length()) {
            char ch = s.charAt(end);
            
            if (map.containsKey(ch)) {
                map.put(ch, map.get(ch)+1);
            } else {
                map.put(ch, 1);
            }
            
            if (map.get(ch) > 1) {
                condition = condition+1;
            }
            
            end = end+1;
            
            while (condition > 0) {
                char sch = s.charAt(start);
                map.put(sch, map.get(sch)-1);
                
                if (map.get(sch) > 0) {
                    condition = 0;
                }
                start = start+1;
            }
            
            max = Math.max(max, end-start);
        }
        
        return max;
    }
}
```

아래 코드에 비해 조금 개선
- end가 마지막에 도달하고 나면 더 이상 추가 계산할 필요 없음
```java  
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
        
        int len = s.length();
        int start = 0;
        int end = 0;
        int max = Integer.MIN_VALUE;
        
        HashMap<Character, Integer> map = new HashMap<>();
        while (end < len) {
            if (!map.containsKey(s.charAt(end)) || map.get(s.charAt(end)) == 0) {                
                map.put(s.charAt(end), 1);
                end = end+1;
            } else {                                
                map.put(s.charAt(start), Math.max(0, map.get(s.charAt(start))-1));
                start++;
            }   
            max = Math.max(max, end-start);
        }
        
        return max;
    }
}
```  

```java  
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
        
        int len = s.length();
        int start = 0;
        int end = 0;
        int max = Integer.MIN_VALUE;
        
        HashMap<Character, Integer> map = new HashMap<>();
        while (start < len) {
            if (end < len 
                && (!map.containsKey(s.charAt(end)) || map.get(s.charAt(end)) == 0)) {                
                map.put(s.charAt(end), 1);
                end = end+1;
            } else {                
                max = Math.max(max, end-start);
                map.put(s.charAt(start), Math.max(0, map.get(s.charAt(start))-1));
                start++;
            }            
        }
        
        return max;
    }
}
```  
