``` java
import java.util.*;

class Solution {
    int[] dx = {0, 1, -1}; // down, right, up
    int[] dy = {1, 0, -1};
    int dir = 0;

    public int[] solution(int n) {
        int[][] array = new int[n][n];

        int indexX = 0, indexY = 0;

        int end = 0;
        for (int i = 1; i <= n; i++) {
            end = end + i;
        }

        for (int i = 1; i <= end; i++) {
            array[indexY][indexX] = i;

            if (isNextIndexValid(indexY, indexX, n, array)) {
                indexY = indexY + dy[dir];
                indexX = indexX + dx[dir];
            } else {
                dir = dir + 1;
                if (dir == 3) dir = 0;

                indexY = indexY + dy[dir];
                indexX = indexX + dx[dir];
            }
        }

        int index = 0;
        int[] answer = new int[end];
        for (int j = 0; j < n; j++) {
            for (int i = 0; i < n; i++) {
                answer[index] = array[j][i];
                index = index + 1;

                if (i + 1 < n && array[j][i + 1] == 0) break;
            }
        }

        return answer;
    }

    private boolean isNextIndexValid(int currentY, int currentX, int n, int[][] array) {
        int nextX = currentX + dx[dir];
        int nextY = currentY + dy[dir];

        return ((0 <= nextX && nextX <= n - 1 && 0 <= nextY  && nextY <= n - 1) && (array[nextY][nextX] == 0));
    }
}
```
