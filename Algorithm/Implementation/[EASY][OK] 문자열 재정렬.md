```` java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int sum = 0;
        String string = sc.next();
        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < string.length(); i++) {
            char ch = string.charAt(i);

            if (Character.isLetter(ch)) {
                sb.append(ch);
            } else {
                sum = sum + (ch - '0');
            }
        }

        char[] charArray = sb.toString().toCharArray();
        Arrays.sort(charArray);

        sb = new StringBuilder();
        for (int i = 0; i < charArray.length; i++) {
            sb.append(charArray[i]);
        }
        sb.append(sum);

        System.out.println(sb.toString());
    }
}
````

````java 
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        String string = sc.next();

        int sum = 0;
        StringBuilder sb = new StringBuilder();
        for (int i=0; i<string.length(); i++) {
            char ch = string.charAt(i);
            if (isNumber(ch)) {
                sum += ch - '0';
            } else {
                sb.append(ch);
            }
        }

        char[] ans = sb.toString().toCharArray();
        Arrays.sort(ans);

        sb = new StringBuilder();
        sb.append(new String(ans));
        sb.append(sum);

        System.out.println(sb.toString());
    }

    private static boolean isNumber(char ch) {
        return '0' <= ch && ch <= '9';
    }
}
````

#### 확인
1. String은 Arrays.sort로 바로 sort 할 수 없기에 char[] array로 변경한 뒤에 정렬해야 한다


``` py
import re

s = input()
chars = re.sub('[0-9]', '', s)
nums = re.sub('[a-zA-Z]', '', s)

sum = 0
for i in range(len(nums)):
    sum += int(nums[i])

result = []
result.append(''.join(sorted(chars)))
result.append(str(sum))

print(''.join(result))
```
