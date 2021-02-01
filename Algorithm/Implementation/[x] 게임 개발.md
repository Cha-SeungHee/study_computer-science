```` java
import java.io.*;
import java.util.*;

class Main {
    static int[] dx = {0, 1, 0, -1};  // up, right, down, left
    static int[] dy = {-1, 0, 1, 0};

    static int N, M, direction, y, x, move, turnCount;
    static int[][] board;
    static boolean[][] visited;

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine(), " ");
        y = Integer.parseInt(st.nextToken());
        x = Integer.parseInt(st.nextToken());
        direction = Integer.parseInt(st.nextToken());

        board = new int[N][M];
        visited = new boolean[N][M];

        for (int j = 0; j < N; j++) {
            st = new StringTokenizer(br.readLine(), " ");

            for (int i = 0; i < M; i++) {
                board[j][i] = Integer.parseInt(st.nextToken());
            }
        }

        move = 1;
        visited[y][x]= true;
        turnCount = 0;

        while (true) {
            direction = direction - 1;
            if (direction == -1) direction = 3;

            int nx = x + dx[direction];
            int ny = y + dy[direction];

            if (isValid(ny, nx)) {
                x = nx;
                y = ny;
                visited[ny][nx] = true;

                move = move + 1;
                turnCount = 0;
            } else {
                turnCount = turnCount + 1;
            }

            if (turnCount == 4) {
                nx = x - dx[direction];
                ny = y - dy[direction];

                if (board[ny][nx] == 0) {
                    x = nx;
                    y = ny;
                } else {
                    break;
                }

                turnCount = 0;
            }
        }

        System.out.println(move);
    }

    private static boolean isValid(int y, int x) {
        return 0 <= y && y <= N - 1 && 0 <= x && x <= M - 1 && !visited[y][x] && board[y][x] == 0;
    }
}
````
