```` java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        st = new StringTokenizer(br.readLine(), " ");

        StringBuilder sb = new StringBuilder();
        while (st.hasMoreTokens()) {
            sb.append(st.nextToken());
        }

        String notes = sb.toString();
        if (notes.equals("12345678")) {
            System.out.println("ascending");
        } else if (notes.equals("87654321")) {
            System.out.println("descending");
        } else {
            System.out.println("mixed");
        }
    }
}
````
