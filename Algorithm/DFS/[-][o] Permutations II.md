```java  
/*
HashMap<Integer, Integer> map
- 숫자 남은 개수 counting 용도

private void permuteHelper(HashMap<Integer, Integer> map, List<List<Integer>> prefix, List<Integer> list, int size) {
    if (list.size() == size) {
        prefix.add(list);
        return;
    }
    
    for (int val : map.keySet()) {
        list.add(val);
        if (map.get(val) == 1) {
            map.remove(val);
            permuteHelper(map, prefix, list, size);
            map.put(val, 1);
        } else {
            map.put(val, map.get(val)-1);
            permuteHelper(map, prefix, list, size);
            map.put(val, map.get(val)+1);
        }
    }
}
*/

class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> permutation = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            permutation.add(new ArrayList<Integer>());
            return permutation; 
        }
        
        
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i=0; i<nums.length; i++) {
            if (map.containsKey(nums[i])) {
                map.put(nums[i], map.get(nums[i])+1);
            } else {
                map.put(nums[i], 1);
            }
        }                
        
        int[] tmp = new int[nums.length];
        permuteHelper(map, permutation, tmp, 0, nums.length);
        
        return permutation;
    }
    
    private void permuteHelper(HashMap<Integer, Integer> map, List<List<Integer>> permutation, int[] tmp, int idx, int size) {
        if (idx == size) {
            List<Integer> list = convertArrayToArrayList(tmp);
            permutation.add(list);
            return;
        }

        for (int val : map.keySet()) {
            if (map.get(val) != 0) {
                tmp[idx] = val;
                map.put(val, map.get(val)-1);
                permuteHelper(map, permutation, tmp, idx+1, size);
                map.put(val, map.get(val)+1);              
            }
        }
    }
    
    private List<Integer> convertArrayToArrayList(int[] array) {
        ArrayList<Integer> list = new ArrayList<>();
        
        for (int i=0; i<array.length; i++) {
            list.add(array[i]);
        }
        
        return list;
    }
}
```

#### 확인 
1. 현재까지의 값을 List에 저장하면 ConcurrentModificationException 발생하여, int[] 배열로 변경하여 
