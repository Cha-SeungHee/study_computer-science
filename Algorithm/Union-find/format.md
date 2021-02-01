``` java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        int[] parent = new int[11];
        
        for (int i = 1; i < parent.length; i++) {
            parent[i] = i;
        }
    }
    
    private static int getParent(int[] parent, int a) {
        if (a == parent[a]) return a;
        
        return parent[a] = getParent(parent, parent[a]);
    }
    
    private static void union(int[] parent, int a, int b) {
        a = getParent(parent, a);
        b = getParent(parent, b);
        
        if (a < b) parent[b] = a;
        if (b < a) parent[a] = b;
    }
    
    private static boolean isUnion(int[] parent, int a, int b) {
        a = getParent(parent, a);
        b = getParent(parent, b);
        
        if (a == b) return true;
        
        return false;
    }
}
```

- parent 배열은 처음엔 자기 자신으로 초기화 -> unionParent 함수를 통해 그래프 연결 상태를 반영하여 업데이트    
- isUnion 함수를 통해서 같은 그래프에 있는지 확인 (찾는 고정에서 getParent 함수에서 추가로 업데이트)   
