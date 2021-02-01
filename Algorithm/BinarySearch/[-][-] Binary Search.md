```java  
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;
        
        int begin = 0, end = nums.length-1;
        
        while (begin <= end) {
            int mid = (begin + end) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > target) {
                end = mid-1;
            } else {
                begin = mid+1;
            }
        }
        
        return -1;
    }
}
```

#### 확인
1. begin <= end에서 = 빼먹음. 이 경우 원소가 하나만 있는 경우 연산 불가.
