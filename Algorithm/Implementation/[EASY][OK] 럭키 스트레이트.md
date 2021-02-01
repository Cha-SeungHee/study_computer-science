````java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int sum = 0;
        String num = sc.next();

        for (int i = 0; i < num.length(); i++) {
            if (i < num.length() / 2) {
                sum = sum + num.charAt(i) - '0';
            } else {
                sum = sum - (num.charAt(i) - '0');
            }
        }

        if (sum == 0) {
            System.out.println("LUCKY");
        } else {
            System.out.println("READY");
        }
    }
}
````

```java 
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        String num = null;
        int sumLeft = 0;
        int sumRight = 0;

        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        num = st.nextToken();

        int len = num.length();
        for (int i=0; i<(len/2); i++) {
            sumLeft += num.charAt(i)-'0';
        }
        for (int i=(len/2); i<len; i++) {
            sumRight += num.charAt(i)-'0';
        }

        String luckyStraight = (sumLeft == sumRight) ? "LUCKY" : "READY";

        bw.write(luckyStraight);
        bw.flush();
    }
}
```
