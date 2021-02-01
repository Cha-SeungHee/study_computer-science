``` java
class Solution {
    public void rotate(int[][] matrix) {
        int len = matrix.length;
        
        for (int d = 0; d < len / 2; d++) {
            for (int k = d; k < len - d - 1; k++) {
                int tmp = matrix[d][k];
                matrix[d][k] = matrix[len - 1 - k][d];
                matrix[len - 1 - k][d] = matrix[len - 1 -d][len - 1 - k];
                matrix[len - 1 -d][len - 1 - k] = matrix[k][len - 1 - d];
                matrix[k][len - 1 - d] = tmp;
            }
        }
    }
}
```
