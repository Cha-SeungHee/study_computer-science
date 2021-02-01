1. Start with pointer left=0 and pointer right=length-1
2. The max water is limited by the pointer with smaller height
3. When moving a pointer, the width of the area decrease
4. If we move the pointer with higher height, we will never get a
greater area, the max height will be at most the one of the pointer with smaller height.
5. So we need to move the pointer with smaller height to have a chance to get higher height at the next step.



```java  
class Solution {
    public int maxArea(int[] height) {
        int left = 0, right = height.length-1, area = 0;                
        
        while (left < right) {            
            area = Math.max(area, Math.min(height[left], height[right])*(right-left));
            if (height[left] <= height[right]) {                                
                left = left+1;                
            } else {                     
                right = right-1;                
            }
        }
        
        return area;
    }
}
```
