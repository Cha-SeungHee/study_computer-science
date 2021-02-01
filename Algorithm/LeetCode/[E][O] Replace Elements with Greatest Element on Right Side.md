``` java
class Solution {
    public int[] replaceElements(int[] arr) {
        if (arr == null || arr.length == 0) return new int[]{};
        
        ArrayList<Integer> list = new ArrayList<>();
        int[] ans = new int[arr.length];
        
        list.add(-1);
        int max = arr[arr.length - 1];
        
        for (int i = arr.length - 2; i >= 0; i--) {                        
            list.add(0, max);
            max = Math.max(max, arr[i]);
        }
        
        for (int i = 0; i < arr.length; i++) {
            ans[i] = list.get(i);
        }
        
        return ans;
    }
}
```
