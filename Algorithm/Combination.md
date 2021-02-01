Combination은 100개의 곡 중 앨범에 들어갈 10곡을 선별하는 것  
순서는 중요하지 않다  

``` java
import java.util.*;

class Main {
    public static void main(String[] args)  {
        int[] arr = {1, 3, 5, 7, 9};
        int r = 3;

        Combination comb = new Combination(arr.length, r);
        comb.combination(arr, 0);
        ArrayList<ArrayList<Integer>> list = comb.getList();

        for (ArrayList<Integer> sublist : list) {
            for (Integer num : sublist) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
    }
}

class Combination {
    private int n;
    private int r;
    ArrayList<Integer> sublist;
    ArrayList<ArrayList<Integer>> list;

    Combination(int n, int r) {
        this.n = n;
        this.r = r;
        sublist = new ArrayList<>();
        list = new ArrayList<>();
    }

    ArrayList<ArrayList<Integer>> getList() {
        return list;
    }

    void combination(int[] arr, int index) {
        if (sublist.size() == r) {
            list.add(new ArrayList<>(sublist));
            return;
        }

        if (index >= arr.length) return;

        sublist.add(arr[index]);
        combination(arr, index + 1);
        sublist.remove(sublist.size() - 1);
        combination(arr, index + 1);
    }
}
```
