```` java
import java.util.*;
import java.io.*;

class Main {
    static int N, M, x, y, K, direction;
    static int[][] board;
    static int[][] dice;

    static int[] dx = {0, 1, -1, 0, 0}; // -, E, W, N, S
    static int[] dy = {0, 0, 0, -1, 1};

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        y = Integer.parseInt(st.nextToken());
        x = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        board = new int[N][M];
        dice = new int[4][3];

        for (int j = 0; j < N; j++) {
            st = new StringTokenizer(br.readLine());

            for (int i = 0; i < M; i++) {
                board[j][i] = Integer.parseInt(st.nextToken());
            }
        }

        st = new StringTokenizer(br.readLine(), " ");
        for (int d = 0; d < K; d++) {
            direction = Integer.parseInt(st.nextToken());
            int nx = x + dx[direction];
            int ny = y + dy[direction];

            if (isValid(ny, nx)) {
                x = nx;
                y = ny;

                rollDice(direction);

                if (board[y][x] == 0) {
                    board[y][x] = dice[3][1];
                } else {
                    dice[3][1] = board[y][x];
                    board[y][x] = 0;
                }

                bw.write(dice[1][1] + "\n");
            }
        }

        bw.flush();

        br.close();
        bw.close();
    }

    private static void rollDice(int direction) {
        int temp;
        switch(direction) {
            case 1:
                temp = dice[3][1];
                dice[3][1] = dice[1][2];
                dice[1][2] = dice[1][1];
                dice[1][1] = dice[1][0];
                dice[1][0] = temp;
                break;

            case 2 :
                temp = dice[3][1];
                dice[3][1] = dice[1][0];
                dice[1][0] = dice[1][1];
                dice[1][1] = dice[1][2];
                dice[1][2] = temp;
                break;

            case 3:
                temp = dice[0][1];
                dice[0][1] = dice[1][1];
                dice[1][1] = dice[2][1];
                dice[2][1] = dice[3][1];
                dice[3][1] = temp;
                break;

            case 4:
                temp = dice[3][1];
                dice[3][1] = dice[2][1];
                dice[2][1] = dice[1][1];
                dice[1][1] = dice[0][1];
                dice[0][1] = temp;
                break;

            default :
                break;
        }
    }

    private static boolean isValid(int y, int x) {
        return 0 <= y && y <= N - 1 && 0 <= x && x <= M - 1;
    }
}
````
