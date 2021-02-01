``` java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int kth = 0;
        Queue<Integer> queue = new PriorityQueue<>((n1, n2) -> (n2 - n1));
        
        for (int num : nums) {
            queue.offer(num);
        }        
        
        for (int i = 0; i < k; i++) {
            kth = queue.poll();
        }
        
        return kth;
    }
}
```

- lambda식  
- PriorityQueue는 기본적으로 ascending  
