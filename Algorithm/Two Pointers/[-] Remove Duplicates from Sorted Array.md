```java  
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0 || nums == null) return 0;
        
        int index = 1;        
        
        for (int i=0; i<nums.length-1; i++) {
            if (nums[i] != nums[i+1]) {
                nums[index] = nums[i+1];
                index = index+1;
            }
        }
        
        return index;
    }
}
```
