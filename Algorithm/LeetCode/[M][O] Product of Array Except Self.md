#### Memory O(n)

``` java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] productFromLeft = new int[nums.length];
        int[] productFromRight = new int[nums.length];
        int[] output = new int[nums.length];
        
        int product = 1;
        for (int i = 0; i < nums.length; i++) {
            product = product * nums[i];
            productFromLeft[i] = product;
        }
        
        product = 1;
        for (int i = nums.length - 1; i >= 0; i--) {
            product = product * nums[i];
            productFromRight[i] = product;
        }
        
        output[0] = productFromRight[1];
        output[nums.length - 1] = productFromLeft[nums.length - 2];
        
        for (int i = 1; i < nums.length - 1; i++) {
            output[i] = productFromLeft[i - 1] * productFromRight[i + 1];
        }
        
        return output;
    }
}
```

Array 하나로도 가능하다  
