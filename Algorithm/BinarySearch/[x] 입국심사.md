```` java
import java.io.*;
import java.util.*;

class Solution {
    public long solution(int n, int[] times) {
        Arrays.sort(times);
        return binerySearch(times, n, times[times.length - 1]);
    }

    long binerySearch(int[] times, int n, long max){
        long left = 1, right = max * n;        
        long ans = Long.MAX_VALUE;        

        while(left <= right){
            long num = 0;
            long mid = (left + right) / 2;

            for (int i = 0; i < times.length; i++){
                num = num + mid / times[i];
            }

            if(num >= n){
                ans = Math.min(ans, mid);
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return ans;
    }
}
````
