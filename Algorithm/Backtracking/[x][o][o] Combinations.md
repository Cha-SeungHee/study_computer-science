```java  
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> list = new ArrayList<>();
        List<Integer> sublist = new ArrayList<>();
        
        boolean[] visited = new boolean[n+1];
        
        combineHelper(list, sublist, 1, visited, k);
        
        return list;    
    }
    
    private void combineHelper(List<List<Integer>> list, List<Integer> sublist, int num, boolean[] visited, int k) {
        if (num >= visited.length) return;
        if (sublist.size() == k) {
            list.add(new ArrayList<>(sublist));
            return;
        }
        
        for (int n = num; n < visited.length; n++) {
            if (!visited[n]) {
                sublist.add(n);
                visited[n] = true;
                combineHelper(list, sublist, n, visited, k);
                visited[n] = false;
                sublist.remove(sublist.size() - 1);
            }
        }
    }
}
```

```java  
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> list = new ArrayList<>();   
        boolean[] visited = new boolean[n+1];
        combineHelper(1, 0, n, k, visited, list);
        
        return list;
    }
    
    private void combineHelper(int cur, int cnt, int n, int k, boolean[] visited, List<List<Integer>> list) {
        if (cnt == k) {
            List<Integer> subList = new ArrayList<>();
            for (int i=1; i<visited.length; i++) {
                if (visited[i]) subList.add(i);
            }
            list.add(subList);
            return;
        }
        
        if (cur == n+1) return;        
        
        for (int i=cur; i<visited.length; i++) {
            if (!visited[i]) {
                visited[i] = true;
                combineHelper(i+1, cnt+1, n, k, visited, list);
                visited[i] = false;
            }
        }
    }
}
```

```java  
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        if (n==0 || k== 0) return null;
        
        List<List<Integer>> list = new ArrayList<>();
        List<Integer> prefix = new ArrayList<>(); 
        combineHelper(list, prefix, 1, n, k);
        
        return list;
    }
    
    private void combineHelper(List<List<Integer>> list, List<Integer> prefix, int cur, int n, int k) {
        if (prefix.size() == k) {
            list.add(new ArrayList<>(prefix));
            return;
        }        
          
        for (int i=cur; i<=n; i++) {
            prefix.add(i);
            combineHelper(list, prefix, i+1, n, k);
            prefix.remove(prefix.size()-1);       
        }   
    }
}
```

#### 확인
1. 중복되는 조합이 없게 하기 위해서 자신보다 큰 값들만 다음 값으로 넘겨주는 방식을 취한다
2. for (int i=0; i<0; i++) 이 경우는 i=0일 때 수행되지 않는다
