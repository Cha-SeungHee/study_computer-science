``` java
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String string = br.readLine();
        int sLen = string.length();

        char prev = 'a';
        int group = 0;

        for (int i = 0; i < sLen; i++) {
            char ch = string.charAt(i);

            if (prev != ch) group = group + 1;

            prev = ch;
        }

        System.out.println(group / 2);
    }
}
```
