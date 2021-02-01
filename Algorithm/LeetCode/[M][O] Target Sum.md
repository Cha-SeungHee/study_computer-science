https://leetcode.com/problems/target-sum/
### DFS/DP 
- index 및 값으로 hash를 생성하기 위해 새로운 클래스를 생성하여 equals, hashCode 메소드를 오버라이드 하기 보다는 String으로 처리  

``` java
class Solution {
    HashMap<String, Integer> map;
    
    public int findTargetSumWays(int[] nums, int S) {
        if (nums == null || nums.length == 0) return 0;
        
        map = new HashMap<>();
        
        return dfs(0, 0, nums, S);
    }
    
    private int dfs(int num, int index, int[] nums, int target) {
        if (index == nums.length) {
            return (num == target) ? 1 : 0;
        }
        
        int count = 0;
        
        String key = getKey(index, num);
        
        if (map.containsKey(key)) {
            count = count + map.get(key);
        } else {
            count = count + dfs(num + nums[index], index + 1, nums, target);
            count = count + dfs(num - nums[index], index + 1, nums, target);
            map.put(key, count);
        }
        
        return count;
    }
    
    private String getKey(int index, int num) {
        return index + "," + num;
    }
}
```



### BFS - 시간 초과
- BFS는 모든 요소에 대해서 하나씩 연산을 같이 하기 때문에 중복 연산이 발생할 수 밖에 없음  
- index가 배열의 끝까지 도달하지 않아도 되면 BFS를 써도 되겠지만 이 경우에는 배열의 끝까지 도달해야 하기 때문에 dp를 활용해야 한다  

``` java
class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        if (nums == null || nums.length == 0) return 0;
        
        int index = 0, count = 0;
        Queue<Integer> queue = new LinkedList<>();
        
        queue.offer(nums[0]);
        queue.offer(-1 * nums[0]);
        
        while (!queue.isEmpty()) {
            index = index + 1; 
            
            int size = queue.size();
            
            for (int k = 0; k < size; k++) {
                int num = queue.poll();
                
                if (index == nums.length) {
                    if (num == S) count = count + 1;
                    
                    continue;
                }
                
                int temp = num + nums[index];
                queue.offer(temp);
                
                temp = num - nums[index];
                queue.offer(temp);  
            }
        }
        
        return count;
    }
}
```
