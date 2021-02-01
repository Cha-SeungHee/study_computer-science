```java  
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        List<Integer> subList = new ArrayList<>();        
        HashMap<Integer, Integer> map = new HashMap<>();
        
        if (nums == null || nums.length == 0) {
            return list;
        }        
        
        for (int i=0; i<nums.length; i++) {
            if (map.containsKey(nums[i])) {
                map.put(nums[i], map.get(nums[i])+1);
            } else {
                map.put(nums[i], 1);
            }
        }        
        
        permuteHelper(list, subList, nums.length, map);
        
        return list;
    }
    
    private void permuteHelper(List<List<Integer>> list, List<Integer> subList, int len, HashMap<Integer, Integer> map)  {
        if (subList.size() == len) {
            List<Integer> newList = new ArrayList<>(subList);
            list.add(newList);
            return;
        }

        for (int num : map.keySet()) {
            if (map.get(num) > 0) {
                subList.add(num);                
                map.put(num, map.get(num)-1);
                permuteHelper(list, subList, len, map);
                subList.remove(subList.size()-1);                
                map.put(num, map.get(num)+1);
            }
        }
    }
}
```
