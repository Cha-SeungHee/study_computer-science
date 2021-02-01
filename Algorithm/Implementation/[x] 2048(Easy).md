```` java
import java.io.*;
import java.util.*;

class Main {
    static int N;
    static int[][] board;
    static int maxSum = 0;

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        N = Integer.parseInt(br.readLine());
        board = new int[N][N];

        for (int j = 0; j < N; j++) {
            st = new StringTokenizer(br.readLine(), " ");

            for (int i = 0; i < N; i++) {
                board[j][i] = Integer.parseInt(st.nextToken());
            }
        }

        backtrack(0, board);

        System.out.println(maxSum);
    }

    private static void backtrack(int count, int[][] board) {
        if (count == 5) {
            int max = 0;
            for (int j = 0; j < board.length; j++) {
                for (int i = 0; i < board[0].length; i++) {
                    max = Math.max(max, board[j][i]);
                }
            }

            maxSum = Math.max(maxSum, max);

            return;
        }

        int[][] temp = copyArray(board);

        for (int direction = 0; direction < 4; direction++) {
            slideBoard(board, direction);

            backtrack(count + 1, board);

            board = copyArray(temp);
        }
    }

    private static int[][] copyArray(int[][] board) {
        int[][] newBoard = new int[board.length][board[0].length];

        for (int j = 0; j < board.length; j++) {
            for (int i = 0; i < board[0].length; i++) {
                newBoard[j][i] = board[j][i];
            }
        }

        return newBoard;
    }

    private static void slideBoard(int[][] board, int direction) {
        boolean[][] added = new boolean[board.length][board[0].length];

        switch(direction) {
            case 0 :
                for (int i = N - 2; i >= 0; i--) {
                    for (int j = 0; j <= N - 1; j++) {
                        if (board[j][i] == 0) continue;

                        if (board[j][i + 1] == 0) {
                            int index = i;

                            while (index + 1 <= N - 1 && board[j][index + 1] == 0) {
                                board[j][index + 1] = board[j][index];
                                board[j][index] = 0;
                                index = index + 1;
                            }

                            if (index + 1 <= N - 1 && !added[j][index + 1] && board[j][index + 1] == board[j][index]) {
                                board[j][index + 1] = board[j][index + 1] * 2;
                                board[j][index] = 0;
                                added[j][index + 1] = true;
                            }
                        } else {
                            if (!added[j][i + 1] && board[j][i + 1] == board[j][i]) {
                                board[j][i + 1] = board[j][i + 1] * 2;
                                board[j][i] = 0;
                                added[j][i + 1] = true;
                            }
                        }
                    }
                }

                break;

            case 1 :
                for (int j = 1; j <= N - 1; j++) {
                    for (int i = 0; i <= N - 1; i++) {
                        if (board[j][i] == 0) continue;

                        if (board[j - 1][i] == 0) {
                            int index = j;

                            while (index - 1 >= 0 && board[index - 1][i] == 0) {
                                board[index - 1][i] = board[index][i];
                                board[index][i] = 0;
                                index = index - 1;
                            }

                            if (index - 1 >= 0 && !added[index - 1][i] && board[index - 1][i] == board[index][i]) {
                                board[index - 1][i] = board[index - 1][i] * 2;
                                board[index][i] = 0;
                                added[index - 1][i] = true;
                            }
                        } else {
                            if (!added[j - 1][i] && board[j - 1][i] == board[j][i]) {
                                board[j - 1][i] = board[j - 1][i] * 2;
                                board[j][i] = 0;
                                added[j - 1][i] = true;
                            }
                        }
                    }
                }

                break;

            case 2 :
                for (int i = 1; i <= N - 1; i++) {
                    for (int j = 0; j <= N - 1; j++) {
                        if (board[j][i] == 0) continue;

                        if (board[j][i - 1] == 0) {
                            int index = i;

                            while (index - 1 >= 0 && board[j][index - 1] == 0) {
                                board[j][index - 1] = board[j][index];
                                board[j][index] = 0;
                                index = index - 1;
                            }

                            if (index - 1 >= 0 && !added[j][index - 1] && board[j][index - 1] == board[j][index]) {
                                board[j][index - 1] = board[j][index - 1] * 2;
                                board[j][index] = 0;
                                added[j][index - 1] = true;
                            }
                        } else {
                            if (!added[j][i - 1] && board[j][i - 1] == board[j][i]) {
                                board[j][i - 1] = board[j][i - 1] * 2;
                                board[j][i] = 0;
                                added[j][i - 1] = true;
                            }
                        }
                    }
                }

                break;

            case 3 :
                for (int j = N - 2; j >= 0; j--) {
                    for (int i = 0; i <= N - 1; i++) {
                        if (board[j][i] == 0) continue;

                        if (board[j + 1][i] == 0) {
                            int index = j;

                            while (index + 1 <= N - 1 && board[index + 1][i] == 0) {
                                board[index + 1][i] = board[index][i];
                                board[index][i] = 0;
                                index = index + 1;
                            }

                            if (index + 1 <= N - 1 && !added[index + 1][i] && board[index + 1][i] == board[index][i]) {
                                board[index + 1][i] = board[index + 1][i] * 2;
                                board[index][i] = 0;
                                added[index + 1][i] = true;
                            }
                        } else {
                            if (!added[j + 1][i] && board[j + 1][i] == board[j][i]) {
                                board[j + 1][i] = board[j + 1][i] * 2;
                                board[j][i] = 0;
                                added[j + 1][i] = true;
                            }
                        }
                    }
                }

                break;

            default :
                break;
        }
    }
}
````
