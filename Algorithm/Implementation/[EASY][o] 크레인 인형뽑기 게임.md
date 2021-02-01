``` java
import java.util.*;

class Solution {
    public int solution(int[][] board, int[] moves) {
        int count = 0;
        int yLen = board.length;
        int xLen = board[0].length;
        
        ArrayList<Stack<Integer>> list = new ArrayList<>();
        
        for (int i = 0; i <= xLen; i++) {
            list.add(new Stack<>());
        }
        
        Stack<Integer> basket = new Stack<>();
        
        for (int j = yLen - 1; j >= 0; j--) {
            for (int i = 0; i < xLen; i++) {
                if (board[j][i] != 0) {
                    list.get(i + 1).push(board[j][i]);
                }
            }
        }
        
        for (int move : moves) {            
            Stack<Integer> stack = list.get(move);
            
            if (!stack.isEmpty()) {
                int num = stack.pop();
                
                if (basket.isEmpty() || (!basket.isEmpty() && basket.peek() != num)) {
                    basket.push(num);
                } else {
                    count = count + 1;
                    
                    while (!basket.isEmpty() && basket.peek() == num) {
                        basket.pop();
                        count = count + 1;
                    }
                }
            }
        }
        
        return count;
    }
}
```
