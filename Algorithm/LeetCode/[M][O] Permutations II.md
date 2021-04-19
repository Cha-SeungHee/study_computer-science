``` py 
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        perm_set = set()
        output = []
        num_list = []
        
        visited = [False] * len(nums)
        
        def dfs(index):
            if index >= len(nums):
                perm_set.add(tuple(num_list.copy()))
                return
            
            for i in range(len(nums)):
                if not visited[i]:
                    num_list.append(nums[i])
                    visited[i] = True
                    dfs(index + 1)
                    num_list.pop()
                    visited[i] = False
                
        dfs(0)        
        
        for num_tuple in perm_set:
            output.append(list(num_tuple))
        
        return output
```

계산 이후 set을 통해서 중복처리를 하는 것이 아니라 계산 과정에서 hash (count)를 이용하면 효율적으로 계산 가능  
