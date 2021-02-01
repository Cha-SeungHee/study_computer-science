#### 정렬 
```java 
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        int[][] ans = new int[K][2];
        
        Arrays.sort(points, (p1, p2) -> (p1[0]*p1[0] + p1[1]*p1[1]) - (p2[0]*p2[0] + p2[1]*p2[1]));
        
        
        for (int i=0; i<K; i++) {
            ans[i][0] = points[i][0];
            ans[i][1] = points[i][1];
        }
        
        return ans;
    }
}
``` 

#### PriorityQueue (Min Heap)
```java 
class Solution {
    public int[][] kClosest(int[][] points, int K) {                            
        Queue<int[]> q = new PriorityQueue<>((p1, p2)->distance(p2)-distance(p1));
        
        for (int[] p : points) {
            q.offer(p);
            if (q.size() > K) {
                q.poll();
            }
        }        
        
        int[][] ans = new int[K][2];
        for (int i=0; i<K; i++) {
            int[] point = q.poll();
            ans[i][0] = point[0];
            ans[i][1] = point[1];
        }
        
        return ans;
    }
    
    private int distance(int[] p) {
        return p[0]*p[0] + p[1]*p[1];
    }
}
``` 

#### MergeSort (시간 초과)
```java 
class Solution {
    public int[][] kClosest(int[][] points, int K) {                            
        mergeSort(points, 0, points.length-1);
        
        int[][] kPoints = new int[K][2];
        
        for (int i=0; i<K; i++) {
            kPoints[i][0] = points[i][0];
            kPoints[i][1] = points[i][1];
        }
        return kPoints;
    }
    
    private void mergeSort(int[][] nums, int begin, int end) {        
        if (begin < end) {
            int mid = begin + (end-begin)/2;
            mergeSort(nums, begin, mid);
            mergeSort(nums, mid+1, end);
            merge(nums, begin, mid, end);    
        }
    }
    
    private void merge(int[][] nums, int begin, int mid, int end) {
        int[][] tmp = new int[nums.length][2];
        int idx = begin;
        int idxLeft = begin;
        int idxRight = mid+1;        
        
        while (idxLeft <= mid && idxRight <= end) {
            if (distance(nums, idxLeft) < distance(nums, idxRight)){
                tmp[idx][0] = nums[idxLeft][0];
                tmp[idx][1] = nums[idxLeft][1];
                idxLeft = idxLeft + 1;
                idx = idx + 1;                
            } else {
                tmp[idx][0] = nums[idxRight][0];
                tmp[idx][1] = nums[idxRight][1];
                idxRight = idxRight + 1;
                idx = idx + 1;   
            }
        }
        
        while (idxLeft <= mid) {
            tmp[idx][0] = nums[idxLeft][0];
            tmp[idx][1] = nums[idxLeft][1];
            idxLeft = idxLeft + 1;
            idx = idx + 1;  
        }
        
        while (idxRight <= end) {
            tmp[idx][0] = nums[idxRight][0];
            tmp[idx][1] = nums[idxRight][1];
            idxRight = idxRight + 1;
            idx = idx + 1;  
        }
        
        for (int i=begin; i<=end; i++) {
            nums[i][0] = tmp[i][0];
            nums[i][1] = tmp[i][1];
        }
    }
    
    private int distance(int[][] points, int idx) {
        return points[idx][0]*points[idx][0] + points[idx][1]*points[idx][1];
    }
}
```
