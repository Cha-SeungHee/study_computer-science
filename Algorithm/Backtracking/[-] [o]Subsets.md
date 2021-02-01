```java  
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        if (nums == null || nums.length == 0) return null;
        
        List<List<Integer>> list = new ArrayList<>();
        int len = nums.length;
        int max = 1<<len;

        for (int i=0; i<max; i++) {
            int k=i;
            int idx = 0;
            List<Integer> tmp = new ArrayList<>();
            while (k>0) {
                if ((k & 1) == 1) {
                    tmp.add(nums[idx]);
                }
                idx += 1;
                k >>= 1;
            }
            list.add(tmp);
        }
        
        return list;
    }
}
```

#### 확인
1. 공집합을 고려해서 시작 index를 0부터 잡아야 한다
