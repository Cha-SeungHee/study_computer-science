``` java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
        
        int start = 0, end = 0, condition = 0, max = Integer.MIN_VALUE;
        HashMap<Character, Integer> map = new HashMap<>();
        
        while (end < s.length()) {
            char ch = s.charAt(end);
            
            if (!map.containsKey(ch)) {
                map.put(ch, 0);
            }
            map.put(ch, map.get(ch) + 1);
            
            if (map.get(ch) > 1) {
                condition = 1;
            }
            
            while (condition > 0) {                
                char chStart = s.charAt(start);
                
                map.put(chStart, map.get(chStart) - 1);
                
                if (map.get(ch) <= 1) {
                    condition = 0;
                }
                
                start = start + 1;
            }
            
            end = end + 1;
            
            max = Math.max(max, end - start);
        }
        
        return max;
    }
}
```
