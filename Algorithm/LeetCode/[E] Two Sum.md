``` java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int[] answer = new int[2];
        
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                answer[0] = i;
                answer[1] = map.get(target - nums[i]);
                break;
            } else {
                map.put(nums[i], i);
            }
        }
        
        return answer;
    }
}
```

``` py
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        result = []
        nums_map = {}
        
        for i in range(len(nums)):
            if target - nums[i] in nums_map:
                result.append(i)
                result.append(nums_map[target - nums[i]])
            else:
                nums_map[nums[i]] = i
        
        return result            
```
