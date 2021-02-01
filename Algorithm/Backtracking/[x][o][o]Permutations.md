```java  
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        List<Integer> sublist = new ArrayList<>();
        
        if (nums == null || nums.length == 0) return list;        
    
        boolean[] visited = new boolean[nums.length];
        
        permuteHelper(list, sublist, nums, visited);
        
        return list;
    }
    
    private void permuteHelper(List<List<Integer>> list, List<Integer> sublist, int[] nums, boolean[] visited) {
        if (sublist.size() == nums.length) {
            list.add(new ArrayList<>(sublist));
        }
        
        for (int i=0; i<nums.length; i++) {
            if (!visited[i]) {
                sublist.add(nums[i]);
                visited[i] = true;
                permuteHelper(list, sublist, nums, visited);
                visited[i] = false;
                sublist.remove(sublist.size()-1);                
            }
        }
    }
}
```

```java  
class Solution {        
    public List<List<Integer>> permute(int[] nums) {        
        if (nums == null) return null;
        
        HashMap<Integer, Boolean> map = new HashMap<>();
        List<Integer> prefix = new ArrayList<>();
        List<List<Integer>> list = new ArrayList<>();
        permuteHelper(nums, map, prefix, list);
        
        return list;
    }
    
    private void permuteHelper(int[] nums, HashMap<Integer, Boolean> map, List<Integer> prefix, List<List<Integer>> list) {
        if (prefix.size() == nums.length) {
            ArrayList<Integer> tmp = new ArrayList<>(prefix);
            list.add(tmp);
            return;
        }
        
        for (int num : nums) {
            if (!map.containsKey(num)){
                prefix.add(num);
                map.put(num, true);
                permuteHelper(nums, map, prefix, list);
                prefix.remove(prefix.size()-1);
                map.remove(num);
            }
        }
    }    
}
```

#### 확인
1. 편의를 위해 String으로 변환하여 permutation을 계산했으나, 음수가 있는 경우 문제가 발생했다.
2. String.substring (0, 0)을 하면 ""이 return 된다.
3. removeLast() -> remove(list.size()-1);

4. List에서 list로 복사하는 방법 : 생성자 활용
new ArrayList<>(anotherList);
