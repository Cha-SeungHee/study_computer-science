#### Constant Space Complexity

``` java
class Solution {
    public int[] singleNumber(int[] nums) {
        if (nums == null || nums.length == 0) return new int[]{};
        
        int[] singleNumberArray;
        ArrayList<Integer> singleNumberList = new ArrayList<>();
        
        Arrays.sort(nums);
        
        for (int i = 0; i < nums.length; ) {
            if (i == nums.length - 1) {
                singleNumberList.add(nums[i]);
                break;
            }
            
            if (nums[i] == nums[i + 1]) {
                i = i + 2;
            } else {
                singleNumberList.add(nums[i]);
                i = i + 1;
            }
        }
        
        singleNumberArray = new int[singleNumberList.size()];
        for (int i = 0; i < singleNumberList.size(); i++) {
            singleNumberArray[i] = singleNumberList.get(i);
        }
        
        return singleNumberArray;
    }
}
```

- nums.length - 1에 대한 예외처리 고려 못함  
- Single Number일 때, Single Number 아닐 때 index 처리  
