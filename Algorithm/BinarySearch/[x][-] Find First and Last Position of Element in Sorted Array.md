``` java
class Solution {
    public int[] searchRange(int[] nums, int target) {        
        return bst(nums, target);
    }
    
    private int[] bst(int[] nums, int target) {
        int[] ans = new int[2];
        
        int indexLeft = lowerBound(nums, target);
        int indexRight = upperBound(nums, target);
        
        ans[0] = indexLeft;
        ans[1] = indexRight;
        
        return ans;
    }
    
    private int lowerBound(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;
        
        int start = 0;
        int end = nums.length - 1;
        
        while (start < end) {
            int mid = start + (end - start) / 2;
            
            if (nums[mid] > target) {
                end = mid - 1;
            } else if (nums[mid] < target) {
                start = mid + 1;
            } else {
                end = mid;
            }
        }        
        
        return (nums[start] == target) ? start : -1;
    }
    
    private int upperBound(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;
        
        int start = 0;
        int end = nums.length - 1;
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            
            if (nums[mid] > target) {
                end = mid - 1;
            } else if (nums[mid] < target) {
                start = mid + 1;
            } else {
                start = mid;
            }
        }
        
        while (start + 1 < nums.length && nums[start + 1] == target) {
            start = start + 1;
        }
        
        return (nums[start] == target) ? start : -1;
    }
}
```
#### 확인
1. leftBound와 rightBound의 차이 발생하는 이유. 
Mid 연산에서 나누기 2를 하게 되면 나머지 값이 버려지게 되는데, 
left bound의 경우 오른쪽 index가 이동하고 반면 (나누기 2했을 때 왼쪽으로 이동하는 효과)
right bound의 경우 왼쪽 index가 이동하다보니 mid값으로 왼쪽 index를 업데이트 하더라도 새로운 mid를 계산했을 때 제자리에 머무를 수 있다.
이로 인해 한칸 전까지만 접근하도록 계산.
