``` java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        if (nums == null || nums.length == 0) return new int[]{};
           
        int[] topKFrequentArray = new int[k];
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int n : nums) {
            if (!map.containsKey(n)) map.put(n, 0);
            map.put(n, map.get(n) + 1);
        }
        
        PriorityQueue<Integer> pq = new PriorityQueue<>((n1, n2) -> {
            if (map.get(n1) > map.get(n2)) {
                return -1;
            } else {
                return 1;
            }
        });
        
        for (int n : map.keySet()) {
            pq.offer(n);
        }
        
        for (int i = 0; i < k; i++) {
            topKFrequentArray[i] = pq.poll();
        }
        
        return topKFrequentArray;
    }
}
```
