### Dequeue
``` java
class Solution {
    public int[] maxSlidingWindow(int[] a, int k) {		
        if (a == null || k <= 0) {
            return new int[0];
        }
        int n = a.length;
        int[] r = new int[n-k+1];
        int ri = 0;
    
        Deque<Integer> q = new ArrayDeque<>();
        for (int i = 0; i < a.length; i++) {
            // remove numbers out of range k
            while (!q.isEmpty() && q.peek() < i - k + 1) {
                q.poll();
            }

            // remove smaller numbers in k range as they are useless
            while (!q.isEmpty() && a[q.peekLast()] < a[i]) {
                q.pollLast();
            }

            // q contains index... r contains content
            q.offer(i);
            if (i >= k - 1) {
                r[ri++] = a[q.peek()];
            }
        }

        return r;
    }
}
```


### PriorityQueue - 시간초과 
``` java
class Solution {    
    public int[] maxSlidingWindow(int[] nums, int k) {        
        int[] maxArray = new int[nums.length - k + 1];
        PriorityQueue<Integer> pq = new PriorityQueue<>((n1, n2) -> {
            return n2 - n1;
        });        
        
        for (int i = 0; i < k; i++) {
            pq.offer(nums[i]);
        }
        
        maxArray[index++] = pq.peek();
        
        for (int i = k; i < nums.length; i++) {
            pq.remove(nums[i - k]);
            pq.offer(nums[i]);
            maxArray[index++] = pq.peek();
        }        
        
        return maxArray;
    }
}
```
