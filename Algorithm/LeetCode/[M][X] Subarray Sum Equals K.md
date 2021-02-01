``` java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int sum = 0, count = 0;
        
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
        
        for (int i = 0; i < nums.length; i++) {
            sum = sum + nums[i];
            
            if (map.containsKey(sum - k)) {
                count = count + map.get(sum - k);
            }
            
            if (!map.containsKey(sum)) {
                map.put(sum, 0);
            }
            map.put(sum, map.get(sum) + 1);
        }
        
        return count;
    }
}
```

핵심 아이디어 
- i까지의 합과 i + n까지의 합의 차이를 구하면 사이 구간의 합을 구할 수 있다  
- 음수가 포함되기에 sliding window 방법으로 접근 불가. start index를 움직였을 때 음수를 빼게 되면 합이 줄어드는 것이 아니라 오히려 증가  
