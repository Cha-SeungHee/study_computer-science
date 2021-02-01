``` java
import java.util.*;
import java.io.*;

class Main {
    static int N;
    static int max = Integer.MIN_VALUE;
    static int min = Integer.MAX_VALUE;
    static ArrayList<Integer> number = new ArrayList<>();
    static HashMap<Character, Integer> map = new HashMap<>();

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine(), " ");
        for (int i = 0; i < N; i++) {
            number.add(Integer.parseInt(st.nextToken()));
        }

        st = new StringTokenizer(br.readLine(), " ");
        map.put('+', Integer.parseInt(st.nextToken()));
        map.put('-', Integer.parseInt(st.nextToken()));
        map.put('*', Integer.parseInt(st.nextToken()));
        map.put('/', Integer.parseInt(st.nextToken()));

        dfs(number.get(0), 1);

        bw.write(max + "\n");
        bw.write(min + "\n");
        bw.flush();
    }

    private static void dfs(int result, int index) {
        if (index == N) {
            min = Math.min(min, result);
            max = Math.max(max, result);
        }

        for (Character ch : map.keySet()) {
            if (map.get(ch) > 0) {
                int newResult = 0;

                switch (ch) {
                    case '+' :
                        map.put(ch, Math.max(0, map.get(ch) - 1));
                        newResult = result + number.get(index);

                        dfs(newResult, index + 1);

                        map.put(ch, map.get(ch) + 1);
                        break;

                    case '-' :
                        map.put(ch, Math.max(0, map.get(ch) - 1));
                        newResult = result - number.get(index);

                        dfs(newResult, index + 1);

                        map.put(ch, map.get(ch) + 1);

                        break;

                    case '*' :
                        map.put(ch, Math.max(0, map.get(ch) - 1));
                        newResult = result * number.get(index);

                        dfs(newResult, index + 1);

                        map.put(ch, map.get(ch) + 1);

                        break;

                    case'/' :
                        map.put(ch, Math.max(0, map.get(ch) - 1));
                        newResult = result / number.get(index);

                        dfs(newResult, index + 1);

                        map.put(ch, map.get(ch) + 1);

                        break;

                    default :
                        break;
                }
            }
        }
    }
}
```
