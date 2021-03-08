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

``` py
import sys

input = sys.stdin.readline

num = input()
zeros = 0
ones = 0

for i in range(1, len(num)):
    if num[i - 1] == '0' and num[i] == '1':
        zeros += 1
    elif num[i - 1] == '1' and num[i] == '0':
        ones += 1

if num[-1] == '0':
    zeros += 1
else:
    ones += 1

print(min(zeros, ones))
```
