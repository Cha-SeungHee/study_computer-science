```java  
class Solution {
    public List<List<Integer>> largeGroupPositions(String s) {        
        int start = 0, end = 0;
        int consecutive = 0;        
        List<List<Integer>> list = new ArrayList<>();
        
        while (end < s.length()) {            
            if (s.charAt(end) == s.charAt(start)) {
                consecutive = consecutive+1;
            } else {
                if (consecutive >= 3) {
                    List<Integer> sublist = new ArrayList<>();
                    sublist.add(start);
                    sublist.add(end-1);
                    list.add(sublist);
                }
                start = end;
                consecutive = 1;
            }
            end = end+1;
        }
        if (consecutive >=3) {
            List<Integer> sublist = new ArrayList<>();
            sublist.add(start);
            sublist.add(end-1);
            list.add(sublist);
        }
        
        return list;            
    }
}
```
