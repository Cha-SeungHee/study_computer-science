Longest Substring Without Repeating Characters.md 기준

```java  
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
        
        HashMap<Character, Integer> map = new HashMap<>();
        int start = 0, end = 0, condition = 0, max = Integer.MIN_VALUE;
        
        while (end < s.length()) {
            // end 이동
            char ch = s.charAt(end);
            
            if (map.containsKey(ch)) {
                map.put(ch, map.get(ch)+1);
            } else {
                map.put(ch, 1);
            }
            // 조건 발생
            if (map.get(ch) > 1) {
                condition = condition+1;
            }
            
            end = end+1;
            
            // 조건 발생시 start 이동                
            while (condition > 0) {
                char sch = s.charAt(start);
                map.put(sch, map.get(sch)-1);
                // 조건이 현재도 유효한지 확인
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
