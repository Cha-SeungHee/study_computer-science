Two pointers - O(n)
```java 
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] ans = new int[2];
        int begin = 0, end = numbers.length-1;
        
        while (begin < end) {
            int sum = numbers[begin] + numbers[end];
            if (sum == target) {
                ans[0] = begin+1;
                ans[1] = end+1;
                
            }
            if (sum < target) {
                begin = begin+1;
            } else {
                end = end-1;
            }
            
        }
        
        return ans;
    }
}
```

탐색 O(2n)
```java 
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] ans = new int[2];
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int i=0; i<numbers.length; i++) {
            map.put(numbers[i], i);
        }
        
        for (int i=0; i<(numbers.length>>1)+1; i++) {
            if (map.containsKey(target-numbers[i])) {
                ans[0] = i+1;
                ans[1] = map.get(target-numbers[i])+1;
                break;
            }
        }
        
        return ans;
    }
}
```

이진검색 - O(nlogn) 시간초과
```java  
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] ans = new int[2];
        for (int i=0; i<numbers.length-1; i++) {
            int result = bst(i+1, numbers.length-1, numbers, target-(numbers[i]));
            if (result != -1) {
                ans[0] = i+1;
                ans[1] = result+1;
                break;
            }
        }
        
        return ans;
    }
    
    private int bst(int begin, int end, int[] numbers, int target) {                
        if (begin <= end) {
            int mid = begin + (end-begin)/2;
            if (numbers[mid] == target) return mid;
            if (numbers[mid] > target) {
                return bst(begin, mid-1, numbers, target);
            } else {
                return bst(begin+1, end, numbers, target);
            }
        }        
        
        return -1;
    }
}
```
