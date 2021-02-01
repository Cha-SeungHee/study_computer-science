```` java
import java.util.*;

class Main {
    public static void main(String[] args) {
        int numA, numB;

        Scanner sc = new Scanner(System.in);
        String stringA = sc.next();
        String stringB = sc.next();

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < stringA.length(); i++) {
            sb.append(stringA.charAt(i));
        }

        numA = Integer.parseInt(sb.reverse().toString());

        sb = new StringBuilder();
        for (int i = 0; i < stringB.length(); i++) {
            sb.append(stringB.charAt(i));
        }


        numB = Integer.parseInt(sb.reverse().toString());

        if (numA > numB) {
            System.out.println(numA);
        } else {
            System.out.println(numB);
        }
    }
}
````
