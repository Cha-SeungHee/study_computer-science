```` java
import java.util.*;

class Solution {
    public int[] solution(int[] answers) {
        int maxCount = 0;
        
        int[] countArray = new int[4];
        int[] studentOne = {1, 2, 3, 4, 5};
        int[] studentTwo = {2, 1, 2, 3, 2, 4, 2, 5};
        int[] studentThree = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};
        int[][] students = new int[4][];
        
        students[1] = studentOne;
        students[2] = studentTwo;
        students[3] = studentThree;
        
        ArrayList<Integer> winnerList = new ArrayList<>();
        
        for (int j = 1; j <= 3; j++) {
            int count = 0;
            int index = 0;
            
            for (int ans : answers) {
                if (students[j][index] == ans) {
                    count = count + 1;
                }
                index = index + 1;
                if (index == students[j].length) index = 0;
            }
            
            countArray[j] = count;
            maxCount = Math.max(maxCount, countArray[j]);
        }
        
        for (int j = 1; j <= 3; j++) {
            if (countArray[j] == maxCount) winnerList.add(j);
        }
        
        int[] winner = new int[winnerList.size()];
        
        for (int i = 0; i < winnerList.size(); i++) {
            winner[i] = winnerList.get(i);
        }
        
        return winner;
    }
}
````
