#### 일반 backtracking

```java  
class Solution {
    public int kSimilarity(String A, String B) {
        if (A == null || B == null) return 0;
        
        return backtrack(0, A.toCharArray(), B);
    }
    
    private int backtrack(int idx, char[] str, String B) {
        String A = new String(str);
        if (A.equals(B) || idx == str.length) {
            return 0;
        } 
        
        if (str[idx] == B.charAt(idx)) {
            return backtrack(idx+1, str, B);
        } else {
            int min = Integer.MAX_VALUE;
            for (int j=idx+1; j<str.length; j++) {
                if (str[j] == B.charAt(idx)) {
                    swap(str, j, idx);
                    min = Math.min(min, backtrack(idx+1, str, B)+1);
                    swap(str, j, idx);
                }
            }
            return min;
        }
    }

    private void swap(char[] str, int idx1, int idx2) {
        char ch = str[idx1];
        str[idx1] = str[idx2];
        str[idx2] = ch;
    }
}
```  


#### Bactracking -> BFS
```java  
class Solution {
    public int kSimilarity(String A, String B) {
        if (A == null || B == null) return 0;
        
        int cnt = 0;
        Queue<String> q = new LinkedList<>();
        Set<String> set = new HashSet<>();
        
        q.offer(A);
        while (!q.isEmpty()) {
            int size = q.size();
            for (int k=0; k<size; k++) {
                String str = q.poll();
                if (str.equals(B)) return cnt;
                
                int i=0;
                while (str.charAt(i) == B.charAt(i)) i++;
                for (int j=i+1; j<B.length(); j++) {
                    if (B.charAt(i) == str.charAt(j)) {
                        String newString = swap(str, i, j);
                        if (set.add(newString)) q.offer(newString);
                    }
                }
            }
            cnt++;
        }
        
        return -1;
    }

    private String swap(String A, int idx1, int idx2) {
        char[] array = A.toCharArray(); 
        char ch = array[idx1];
        array[idx1] = array[idx2];
        array[idx2] = ch;
        
        return new String(array);
    }
}
```

Set을 이용한 중복처리 제거가 포인트
