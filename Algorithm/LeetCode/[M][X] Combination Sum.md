### dp (top-down)
``` java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        if (candidates == null || candidates.length == 0) return new ArrayList<>();        
        
        Arrays.sort(candidates);
        
        List<List<Integer>>[] dp = new ArrayList[target + 1];
        
        return combinationHelper(dp, candidates, target);
    }
    
    private List<List<Integer>> combinationHelper(List<List<Integer>>[] dp, int[] candidates, int target) {
        if (dp[target] != null) return dp[target];        
        
        List<List<Integer>> list = new ArrayList<>();
        
        for (int num : candidates) {
            if (target < num) continue;
            
            if (num == target) {
                List<Integer> sublist = new ArrayList<>();
                sublist.add(num);                
                list.add(sublist);
            }
            
            List<List<Integer>> prevList = combinationHelper(dp, candidates, target - num);
            for (List<Integer> prev : prevList) {
                if (prev.get(0) >= num) {
                    List<Integer> newList = new ArrayList<>();
                    newList.add(num);
                    newList.addAll(prev);                    
                    list.add(newList);                    
                }
            }
        }
        
        dp[target] = list;
        
        return dp[target];
    }
}
```
- dp의 데이터형 및 배열 생성 방법 확인  
- 중복을 제거하기 위해 맨 앞 값보다 작은 경우에만 값을 비교하도록 하며 새로 값을 추가할 때는 맨 앞에 값을 삽입  
``` java
for (List<Integer> prev : prevList) {
    if (prev.get(0) >= num) {
        List<Integer> newList = new ArrayList<>();
        newList.add(num);
        newList.addAll(prev);                    
        list.add(newList);                    
    }
}
```


### backtracking

``` java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        if (candidates == null || candidates.length == 0) return new ArrayList<>();
        
        List<List<Integer>> list = new ArrayList<>();
        List<Integer> subList = new ArrayList<>();
        HashSet<List<Integer>> listSet = new HashSet<>();
        
        combinationHelper(list, subList, listSet, candidates, target);
        
        return list;
    }
    
    private void combinationHelper(List<List<Integer>> list, List<Integer> subList, HashSet<List<Integer>> listSet, int[] candidates, int target) {
        if (target < 0) return;
        
        if (target == 0) {
            List<Integer> tempList = new ArrayList<>(subList);
            Collections.sort(tempList);
            
            if (listSet.add(tempList)) list.add(tempList);                            
            return;            
        }        
        
        for (int num : candidates) {
            subList.add(num);
            combinationHelper(list, subList, listSet, candidates, target - num);
            subList.remove(subList.size() - 1);
        }
    }
}
```

- HashSet의 type으로 List 사용 가능  
