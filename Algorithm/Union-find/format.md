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

``` py
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)

    if a < b:
        parent[b] = a
    else:
        parent[a] = b

v, e = map(int, input().split())
parent = [0] * (v + 1)

for i in range(1, v + 1):
    parent[i] = i

cycle = False

for i in range(e):
    a, b = map(int, input().split())

    if find_parent(parent, a) == find_parent(parent, b):
        cycle = True
        break
    else:
        union_parent(parent, a, b)

if cycle:
    print('사이클 발생')
else:
    print('사이클 발생 x')
```
