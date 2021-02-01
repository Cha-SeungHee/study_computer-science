```java  
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        if (s.length() < p.length()) return new ArrayList<>();
        
        int start = 0, end = 0, count = 0;
        ArrayList<Integer> list = new ArrayList<>();
        HashMap<Character, Integer> map = new HashMap<>();
        
        for (int i=0; i<p.length(); i++) {
            char ch = p.charAt(i);
            if (map.containsKey(ch)) {
                map.put(ch, map.get(ch)+1);
            } else {
                map.put(ch, 1);
                count = count+1;
            }
        }       
        
        while (end < s.length()) {
            char charEnd = s.charAt(end);
            if (map.containsKey(charEnd)) {
                map.put(charEnd, map.get(charEnd)-1);
                if (map.get(charEnd) == 0) count = count-1;    
            }           
            
            if (count == 0) list.add(start);
            
            if (end-start >= p.length()-1) {                                
                char charStart = s.charAt(start);           
                if (map.containsKey(charStart)) {
                    map.put(charStart, map.get(charStart)+1);
                    if (map.get(charStart) > 0) count = count+1;
                }
                start = start+1;
            }
            
            end = end+1;
        }
        
        return list;
    }
}
```

아래 방법은 매 글자 이동할 때마다 anagram 여부를 모든 글자를 순회하면서 파악하기 때문에 sliding window가  

```java  
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        if (s.length() < p.length()) return new ArrayList<>();
        
        int start = 0, end = 0, condition = 0;
        ArrayList<Integer> indice = new ArrayList<>();
        HashMap<Character, Integer> count = new HashMap<>();
        
        for (int i=0; i<p.length(); i++) {
            if (!count.containsKey(p.charAt(i))) {
                count.put(p.charAt(i), 1);    
            } else {
                count.put(p.charAt(i), count.get(p.charAt(i))+1); 
            }
        }
        
        while (end < s.length()) {            
            char charEnd = s.charAt(end);
            if (end < p.length()-1) {
                if (count.containsKey(charEnd)) count.put(charEnd, count.get(charEnd)-1);
            } else {                
                if (count.containsKey(charEnd)) count.put(charEnd, count.get(charEnd)-1);
                if (isValid(count)) indice.add(start);
                
                char charStart = s.charAt(start);
                if (count.containsKey(charStart)) count.put(charStart, count.get(charStart)+1);
                start = start+1;
            }
            end = end+1;
        }
        
        return indice;
    }
    
    private boolean isValid(HashMap<Character, Integer> count) {
        boolean isValid = true;
        for (Character ch : count.keySet()) {
            if (count.get(ch) > 0) {
                isValid = false;
                break;
            }
        }
        
        return isValid;
    }
}
```
