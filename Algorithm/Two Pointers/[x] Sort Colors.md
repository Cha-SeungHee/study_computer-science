```java  
class Solution {
    public void sortColors(int[] nums) {
        int left = 0, right = nums.length-1;        
        
        for (int i=0; i<=right; i++) {
            if (nums[i] == 0 && i != left) {
                swap(nums, i, left);
                left = left+1;
                i = i-1;
            } else if (nums[i] == 2 && i != right) {
                swap(nums, i, right);
                right = right-1;
                i = i-1;
            }
        }
    }
    
    private void swap(int[] nums, int index1, int index2) {
        int temp = nums[index1];
        nums[index1] = nums[index2];
        nums[index2] = temp;
    }
}
```
