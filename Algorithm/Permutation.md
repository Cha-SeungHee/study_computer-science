Permutation은 순서대로 앨범에 들어갈 10가지 음악의 순서를 정하는 것.  
그렇기에 가능한 모든 조합을 출력한다  

#### visited 없이 최적화
지금까지 방문한 요소들을 왼쪽부터 차곡차곡 쌓아가면서 이후에는 해당 노드의 오른쪽만 탐색함으로써 visited를 사용하지 않음  
visited에 비해 불필요한 탐색을 감소  

``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        int[] arr = {1, 3, 5, 7, 9};
        Permutation perm = new Permutation(arr.length, 3);
        perm.permute(arr, 0);
        ArrayList<ArrayList<Integer>> list = perm.getList();
        System.out.println(list.size());
        for (ArrayList<Integer> sub : list) {
            for (Integer num : sub) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
    }
}

class Permutation {
    private int n;
    private int r;
    private ArrayList<Integer> sublist;
    private ArrayList<ArrayList<Integer>> list;

    public ArrayList<ArrayList<Integer>> getList() {
        return list;
    }

    Permutation(int n, int r) {
        this.n = n;
        this.r = r;
        sublist = new ArrayList<>();
        list = new ArrayList<>();
    }

    void swap(int[] arr, int index1, int index2) {
        int tmp = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = tmp;
    }

    void permute(int[] arr, int index) {
        if (sublist.size() == r) {
            list.add(new ArrayList<>(sublist));
            return;
        }

        for (int i = index; i < n; i++) {
            swap(arr, index, i);
            sublist.add(arr[index]);
            permute(arr, index + 1);
            sublist.remove(sublist.size() - 1);
            swap(arr, index, i);
        }
    }
}
```

#### visited 활용
``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        int[] arr = {1, 3, 5, 7, 9};
        Permutation perm = new Permutation(arr.length, 3);
        perm.permute(arr);
        ArrayList<ArrayList<Integer>> list = perm.getList();
        System.out.println(list.size());
        for (ArrayList<Integer> sub : list) {
            for (Integer num : sub) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
    }
}

class Permutation {
    private int n;
    private int r;
    private boolean[] visited;
    private ArrayList<Integer> sublist;
    private ArrayList<ArrayList<Integer>> list;

    public ArrayList<ArrayList<Integer>> getList() {
        return list;
    }

    Permutation(int n, int r) {
        this.n = n;
        this.r = r;
        visited = new boolean[n];
        sublist = new ArrayList<>();
        list = new ArrayList<>();
    }

    void permute(int[] arr) {
        if (sublist.size() == r) {
            list.add(new ArrayList<>(sublist));
            return;
        }

        for (int i=0; i<arr.length; i++) {
            if (!visited[i]) {
                visited[i] = true;
                sublist.add(arr[i]);
                permute(arr);
                sublist.remove(sublist.size() - 1);
                visited[i] = false;
            }
        }
    }
}
```
