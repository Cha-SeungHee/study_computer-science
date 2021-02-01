```` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException{
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int N = Integer.parseInt(br.readLine());

        ArrayList<Person> list = new ArrayList<>();

        for (int i = 0 ; i < N; i++) {
            st = new StringTokenizer(br.readLine());

            int weight = Integer.parseInt(st.nextToken());
            int height = Integer.parseInt(st.nextToken());

            list.add(new Person(weight, height));
        }

        for (int i = 0; i < N; i++) {
            int rank = 1;
            Person p1 = list.get(i);
            Person p2 = p1;

            for (int j = 0; j < N; j++) {
                if (i == j) continue;

                p2 = list.get(j);
                if (p1.height < p2.height && p1.weight < p2.weight) rank = rank + 1;
            }

            p1.rank = rank;
        }

        for (Person person : list) {
            bw.write(person.rank + " ");
        }
        bw.write("\n");
        bw.flush();
    }

    static class Person {
        int height, weight, rank;

        Person(int weight, int height) {
            this.weight = weight;
            this.height = height;
        }
    }
}
````
