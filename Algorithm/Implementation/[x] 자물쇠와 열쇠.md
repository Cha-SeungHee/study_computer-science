``` java
import java.util.*;

class Solution {
    public boolean solution(int[][] key, int[][] lock) {
        int lenLock = lock.length;
        int lenKey = key.length;
        int[][] newLock = new int[lenLock * 3][lenLock * 3];
        
        for (int j = 0; j < lenLock; j++) {
            for (int i = 0; i < lenLock; i++) {
                newLock[lenLock + j][lenLock + i] = lock[j][i];
            }
        }
        
        for (int rotation = 0; rotation < 4; rotation++) {
            key = rotate(key);
            
            for (int y = 0; y < 2 * lenLock; y++) {
                for (int x = 0; x < 2 * lenLock; x++) {
                    for (int j = 0; j < lenKey; j++) {
                        for (int i = 0; i < lenKey; i++) {
                            newLock[y + j][x + i] += key[j][i];
                        }
                    }
                    
                    if (check(newLock)) return true;
                    
                    for (int j = 0; j < lenKey; j++) {
                        for (int i = 0; i < lenKey; i++) {
                            newLock[y + j][x + i] -= key[j][i];
                        }
                    }
                }
            }
            
        }        
        
        return false;
    }
    
    private boolean check(int[][] newLock) {
        int len = newLock.length / 3;
        
        for (int j = len; j < 2 * len; j++) {
            for (int i = len; i < 2 * len; i++) {
                if (newLock[j][i] != 1) {
                    return false;
                }
            }
        }
        
        return true;
    }
    
    private int[][] rotate(int[][] a) {
        int yLen = a.length;
        int xLen = a[0].length;
        
        int[][] rotation = new int[xLen][yLen];
        
        for (int j=0; j<yLen; j++) {
            for (int i=0; i<xLen; i++) {
                rotation[i][j] = a[yLen - 1 - j][i];
            }
        }
        
        return rotation;
    }
}
```

#### 확인 
1. rotation   
2. 완전 탐색으로 가능한지 판별하기 위한 시간복잡도 계산  
