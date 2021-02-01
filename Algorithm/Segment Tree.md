```java 
import java.util.*;
import java.io.*;

class Main {
    static int[] a = {1, 9, 3, 8, 4, 5, 5, 9, 10, 3, 4, 5};
    static int[] tree = new int[4 * a.length];

    public static void main(String[] args) {
        init(0, a.length-1, 1);
        System.out.println(sum(0, a.length-1, 1, 0, 12));
        System.out.println(sum(0, a.length-1, 1, 3, 8));
        update(0, a.length-1, 1, 5, -5);
        System.out.println(sum(0, a.length-1, 1, 3, 8));
    }

    /*
    Tree의 노드에서 어떤 index의 범위를 커버하는지 값을 저장하는 것이 아니라
    재귀로 탐색할 때마다 start, end값을 변경해주어 해당 node가 포함하는 범위를 변경해준다
    그렇기에 start, end, node는 항상 인자로써 같이 다녀야 한
     */

    /*
    start: 시작 index  end: 끝 index
    */
    static int init(int start, int end, int node) {
        if (start == end) return tree[node] = a[start];

        int mid = start + (end-start)/2;

        return tree[node] = init(start, mid, node*2) + init(mid+1, end, node*2+1);
    }

    /*
    start: 시작 index  end: 끝 index
    left, right: 구간 합을 구하고자 하는 범위 - 재귀 내에서 변하지 않음
     */
    static int sum(int start, int end, int node, int left, int right) {
        if (left > end || right < start) return 0;

        if (left <= start && end <= right) return tree[node];

        int mid = start + (end - start) / 2;

        return sum(start, mid, node*2, left, right) + sum(mid+1, end, node*2+1, left, right);
    }

    static void update(int start, int end, int node, int index, int diff) {
        if (index < start || index > end) return;

        tree[node] += diff;
        if (start == end) return;
        int mid = start + (end-start)/2;
        update(start, mid, node*2, index, diff);
        update(mid+1, end, node*2, index, diff);
    }
}
```
