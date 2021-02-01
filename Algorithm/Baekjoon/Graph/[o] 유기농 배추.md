```java  
import java.io.*;
import java.util.*;

class Main {
    static int[] dx = {1, 0, -1, 0}; // right, up, left, down
    static int[] dy = {0, -1, 0, 1};

    public static void main(String args[]) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int testCase = Integer.parseInt(br.readLine());
        for (int i=0; i<testCase; i++) {
            runTest(br);
        }
    }

    private static void runTest(BufferedReader br) throws IOException{
        StringTokenizer st;
        st = new StringTokenizer(br.readLine(), " ");
        int xLen = Integer.parseInt(st.nextToken());
        int yLen = Integer.parseInt(st.nextToken());
        int num = Integer.parseInt(st.nextToken());
        int numLand = 0;

        int[][] land = new int[yLen][xLen];
        boolean[][] visited = new boolean[yLen][xLen];

        for (int i=0; i<num; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            land[y][x] = 1;
        }

        for (int j=0; j<yLen; j++) {
            for (int i=0; i<xLen; i++) {
                if (!visited[j][i] && land[j][i] == 1) {
                    bfs(i, j, xLen, yLen, land, visited);
                    numLand = numLand+1;
                }
            }
        }

        System.out.println(numLand);
    }

    private static void bfs(int x, int y, int xLen, int yLen, int[][] land, boolean[][] visited) {
        Queue<Point> queue = new LinkedList<>();
        visited[y][x] = true;
        queue.offer(new Point(x, y));
        while (!queue.isEmpty()) {
            Point point = queue.poll();
            for (int k=0; k<4; k++) {
                int tmpX = point.x + dx[k];
                int tmpY = point.y + dy[k];

                if (isValid(tmpX, tmpY, xLen, yLen)) {
                    if (!visited[tmpY][tmpX] && land[tmpY][tmpX] == 1) {
                        queue.offer(new Point(tmpX, tmpY));
                    }
                    visited[tmpY][tmpX] = true;
                }

            }
        }
    }

    private static boolean isValid(int x, int y, int xLen, int yLen) {
        return 0 <= x && x <= xLen-1 && 0 <= y && y <= yLen-1;
    }

    static class Point {
        int x;
        int y;

        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
}
``` 
