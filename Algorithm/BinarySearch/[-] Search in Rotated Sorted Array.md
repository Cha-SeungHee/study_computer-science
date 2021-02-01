
```java  
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;
        
        return bst(nums, 0, nums.length-1, target);
    }
    
    private int bst(int[] nums, int start, int end, int target) {
        if (start > end) return -1;
        if (start <= end) {            
            int mid = (start+end)>>1;     
            if (nums[mid] == target) return mid;                     
            
            // 왼쪽이 정상
            if (nums[start] <= nums[mid]) {
                if (nums[start] <= target && target <= nums[mid]) {                    
                    return bst(nums, start, mid-1, target);
                } else {
                    return bst(nums, mid+1, end, target);
                }
            } 
            
            // 오른쪽이 정상
            if (nums[mid] <= nums[end]) {
                if (nums[mid] <= target && target <= nums[end]) {
                    return bst(nums, mid+1, end, target);
                } else {
                    return bst(nums, start, mid-1, target);
                }
            }
        }
        
        return -1;
    }
}
```

```java  
class Solution {
    public int search(int[] nums, int target) {
        int start = 0;
        int end = nums.length-1;
        
        while (start <= end) {
            int mid = start + (end-start)/2;
            if (nums[mid] == target) return mid;
            
            //좌측이 정렬
            if (nums[start] <= nums[mid]) {
                if (nums[start] <= target && target < nums[mid]) {
                    end = mid-1;
                } else {
                    start = mid+1;
                }
            }
            
            // 우측이 정렬
            if (nums[mid] <= nums[end]) {
                if (nums[mid] < target && target <= nums[end]) {
                    start = mid+1;
                } else {
                    end = mid-1;
                }
            }
        }
        
        return -1;
    }
}
```

#### 확인
1. 경계값에 대한 고민 필요
2. Rotate 되지 않은 정상적으로 정렬된 부분을 판단하여 target이 있는 방향 
