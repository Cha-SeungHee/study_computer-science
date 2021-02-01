```` java 
import java.util.*;

class Main {
    static int[] dx = {2, 2, -2, -2, -1, 1, -1, 1};
    static int[] dy = {-1, 1, -1, 1, -2, -2, 2, 2};

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String start = sc.next();

        int count = 0;

        int x = start.charAt(0) - 'a';
        int y = Integer.parseInt(start.substring(1, 2)) - 1;

        for (int k = 0; k < 8; k++) {
            int nx = x + dx[k];
            int ny = y + dy[k];

            if (isValid(nx, ny)) count++;
        }

        System.out.println(count);
    }

    private static boolean isValid(int x, int y) {
        return 0 <= x && x <= 7 && 0 <=y && y <= 7;
    }
}
````
