``` py
import heapq


class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        num_dict = {}
        heap = []
        
        begin, end, count = 0, k - 1, k                 
        result = []
        
        for i in range(count):
            num_dict[nums[i]] = num_dict.get(nums[i], 0) + 1
            heapq.heappush(heap, -nums[i])
        
        while end < len(nums):            
            while num_dict[-heap[0]] == 0:                
                remove = -heapq.heappop(heap)  
            result.append(-heap[0])
            
            end += 1            
            if end < len(nums):
                num_dict[nums[end]] = num_dict.get(nums[end], 0) + 1
                heapq.heappush(heap, -nums[end])
                num_dict[nums[begin]] = max(0, num_dict[nums[begin]] - 1)
                begin += 1
            
        return result
```

deque을 활용한 좀 더 효율적인 풀이 - o(n)
``` py
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        result = []
        q = collections.deque()
        l = r = 0
        
        while r < len(nums):
            while q and nums[q[-1]] < nums[r]:
                q.pop()
            q.append(r)
            
            while l > q[0]:
                q.popleft()
                        
            if (r + 1) >= k:
                result.append(nums[q[0]])
                l += 1
                
            r += 1
            
        return result
```
