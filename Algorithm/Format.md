#### Input
``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        int N = Integer.parseInt(st.nextToken());

    }
}
```

#### Node
``` java
class Node {
    int y, x;

    Node(int y, int x) {
        this.y = y;
        this.x = x;
    }
}
```

#### Combination
``` java
class Combination {
    private int n, r;
    private ArrayList<Node> sublist;
    private ArrayList<ArrayList<Node>> list;

    Combination(int n, int r) {
        this.n = n;
        this.r = r;
        sublist = new ArrayList<>();
        list = new ArrayList<>();
    }

    void combine(ArrayList<Node> source, int index) {
        if (sublist.size() == r) {
            list.add(new ArrayList<>(sublist));
            return;
        }

        if (index == n) return;

        sublist.add(source.get(index));
        combine(source, index + 1);
        sublist.remove(sublist.size() - 1);
        combine(source, index + 1);
    }

    ArrayList<ArrayList<Node>> getList() {
        return list;
    }
}
```

