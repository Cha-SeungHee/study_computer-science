```java 
class Solution {
    public int majorityElement(int[] nums) {
        return helper(nums, 0, nums.length-1);
    }
    
    private int helper(int[] nums, int begin, int end) {        
        if (begin == end) return nums[begin];
        
        if (begin < end) {
            int mid = begin + (end-begin)/2;
        
            int left = helper(nums, begin, mid);
            int right = helper(nums, mid+1, end);    
            
            int cntLeft = 0;
            int cntRight = 0;
            for (int i=begin; i<=end; i++) {
                if (nums[i] == left) cntLeft++;
                if (nums[i] == right) cntRight++;
            }
            
            return (cntLeft >= cntRight) ? left : right;
        }
        
        return -1;
    }
}
```

```java 
class Solution {
    public int majorityElement(int[] nums) {
        return majorityHelper(nums, 0, nums.length-1);
    }
    
    private int majorityHelper(int[] nums, int begin, int end) {
        if (begin == end) {
            return nums[begin];
        }
        
        int mid = begin + (end-begin)/2;
        int left = majorityHelper(nums, begin, mid);
        int right = majorityHelper(nums, mid+1, end);
        
        if (left == right) return left;
        
        int leftCount = countInRange(nums, left, begin, end);
        int rightCount = countInRange(nums, right, begin, end);
        
        if (leftCount > rightCount) return left;
        
        return right;
    }
    
    private int countInRange(int[] nums, int num, int begin, int end) {
        int cnt = 0;
        
        for (int i=begin; i<=end; i++) {
            if (nums[i] == num) cnt++;
        }
        
        return cnt;
    }
}
```

#### 확인
1. 직관적으로 왼쪽과 오른쪽에서 가장 많은 개수의 숫자를 추려낸 뒤에 가장 많은 개수의 숫자를 찾는 방식인데, 예외가 있지 않을까 조금 깨름칙하다...

Intuition
If we know the majority element in the left and right halves of an array, we can determine which is the global majority element in linear time.
