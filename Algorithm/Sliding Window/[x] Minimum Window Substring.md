자료구조에 따라서 풀이가 훨씬 간단해질 수 있음

```java  
class Solution {
    public String minWindow(String s, String t) {
        if (s.length() < t.length()) return "";
        
        int start = 0, end = 0, count = t.length();
        String ans = null;
        HashMap<Character, Integer> map = new HashMap<>();
        
        for (int i=0; i<t.length(); i++) {
            char ch = t.charAt(i);
            if (map.containsKey(ch)) {
                map.put(ch, map.get(ch)+1);               
            } else {
                map.put(ch, 1);
            }
        }
        
        while (end < s.length()) {
            char charEnd = s.charAt(end);
            if (map.containsKey(charEnd)) {
                map.put(charEnd, map.get(charEnd)-1);
                if (map.get(charEnd) >= 0) {
                    count = count-1;
                }    
            }
            end = end+1;            
            
            while (count == 0) {
                char charStart = s.charAt(start);                
                if (map.containsKey(charStart)) {
                    String tmp = s.substring(start, end);
                    if (ans == null || ans.length() > tmp.length()) {
                        ans = tmp;
                    }

                    map.put(charStart, map.get(charStart)+1);
                    if (map.get(charStart) > 0) {
                        count = count+1;
                    }                        
                }
                start = start+1;
            }
        }
        
        return (ans == null) ? "" : ans;        
    }
}
```  

중복에 대한 고려 실패
자료 구조 너무 복잡

```java  

/* 예외 처리 
s length < t length

현재 포함된 글자의 종류 in
현재 포함되지 않은 글자의 종류 out
현재 글자의 개수 count

모든 글자를 포함시키는지 여부
- out이 empty인지 확인
*/

class Solution {
    public String minWindow(String s, String t) {
        if (s.length() < t.length()) return "";
        
        HashMap<Character, Integer> count = new HashMap<>();
        HashSet<Character> in = new HashSet<>();
        HashSet<Character> out = new HashSet<>();
        int start = 0, end = 0, condition = 0;
        String ret = null;
        
        // t의 모든 글자는 현재 포함되지 않음
        for (int i=0; i<t.length(); i++) {
            char ch = t.charAt(i);
            out.add(ch);
            count.put(ch, 0);
        }
        
        while (end < s.length()) {
            // end 이동시키면서 모든 글자가 포함되어 있는지 확인
            char charEnd = s.charAt(end);
            if (isValidLetter(charEnd, t)) {
                in.add(charEnd);
                count.put(charEnd, count.get(charEnd)+1);
                out.remove(charEnd);
            }
            if (out.size() == 0) {
                condition = condition+1;
            }
            end = end+1;
            
            while (condition > 0) {
                String tmp = s.substring(start, end);
                if (ret == null || tmp.length() < ret.length()) {
                    ret = tmp;
                }
                
                char charStart = s.charAt(start);
                if (isValidLetter(charStart, t)) {
                    // System.out.println("start : " + start + " end : " + end + " ret : " + ret);                                                    
                    // System.out.println(count.get(charStart));
                    count.put(charStart, Math.max(0, count.get(charStart)-1));
                    // System.out.println(count.get(charStart));
                    // System.out.println();
                    if (count.get(charStart) == 0) {
                        out.add(charStart);
                        in.remove(charStart);
                    }
                    if (out.size() > 0) {
                        condition -= 1;
                    }    
                }
                
                start = start+1;
            }
            
            
        }
        
        return (ret == null) ? "" : ret;
    }
    
    private boolean isValidLetter(char ch, String str) {
        boolean isValid = false;
        char[] charArray = str.toCharArray();
        for (char character : charArray){
            if (ch == character) {
                isValid = true;
                break;
            }
        }
        
        return isValid;
    }
}
```
