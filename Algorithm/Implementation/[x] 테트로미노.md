
#### 시간초과
```` java
import java.util.*;
import java.io.*;

class Main {
    static int N, M;

    static int[][] board;
    static int[][] type1 = new int[4][4];
    static int[][] type2 = new int[2][2];
    static int[][] type3 = new int[3][3];
    static int[][] type4 = new int[3][3];
    static int[][] type5 = new int[3][3];

    static int max = Integer.MIN_VALUE;

    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        board = new int[N][M];

        for (int j = 0; j < N; j++) {
            st = new StringTokenizer(br.readLine(), " ");

            for (int i = 0; i < M; i++) {
                board[j][i] = Integer.parseInt(st.nextToken());
            }
        }

        type1[0][0] = 1;
        type1[0][1] = 1;
        type1[0][2] = 1;
        type1[0][3] = 1;

        type2[0][0] = 1;
        type2[0][1] = 1;
        type2[1][0] = 1;
        type2[1][1] = 1;

        type3[0][0] = 1;
        type3[1][0] = 1;
        type3[2][0] = 1;
        type3[2][1] = 1;

        type4[0][0] = 1;
        type4[1][0] = 1;
        type4[1][1] = 1;
        type4[2][1] = 1;

        type5[1][0] = 1;
        type5[1][1] = 1;
        type5[1][2] = 1;
        type5[2][1] = 1;

        ArrayList<int[][]> list = new ArrayList<>();
        list.add(type1);
        list.add(type2);
        list.add(type3);
        list.add(type4);
        list.add(type5);

        for (int k = 0; k < list.size(); k++) {
            int[][] type = list.get(k);
            int yLen = type.length;
            int xLen = type[0].length;

            for (int j = 0; j <= N - yLen; j++) {
                for (int i = 0; i <= M - xLen; i++) {
                    for (int xs = 0; xs < 2; xs++ ){
                        type = xSymmetry(type);

                        for (int r = 0; r < 4; r++) {
                            type = rotate(type);

                            int tempMax = 0;
                            for (int ny = 0; ny < yLen; ny++) {
                                for (int nx = 0; nx < xLen; nx++) {
                                    if (type[ny][nx] == 1) {
                                        tempMax = tempMax + board[ny + j][nx + i];
                                    }
                                }
                            }

                            max = Math.max(max, tempMax);
                        }
                    }

                    for (int ys = 0; ys < 2; ys++) {
                        type = ySymmetry(type);

                        for (int r = 0; r < 4; r++) {
                            type = rotate(type);
                        }
                    }
                }
            }
        }

        System.out.println(max);
    }

    private static int[][] xSymmetry(int[][] type) {
        int yLen = type.length;
        int xLen = type[0].length;

        int[][] newType = new int[yLen][xLen];

        for (int j = 0; j < yLen; j++) {
            for (int i = 0; i < xLen; i++) {
                newType[yLen - 1 - j][i] = type[j][i];
            }
        }

        return newType;
    }

    private static int[][] ySymmetry(int[][] type) {
        int yLen = type.length;
        int xLen = type[0].length;

        int[][] newType = new int[yLen][xLen];

        for (int j = 0; j < yLen; j++) {
            for (int i = 0; i < xLen; i++) {
                newType[j][xLen - 1 - i] = type[j][i];
            }
        }

        return newType;
    }

    private static int[][] rotate(int[][] type) {
        int yLen = type.length;
        int xLen = type[0].length;

        int[][] newType = new int[xLen][yLen];

        for (int j = 0; j < yLen; j++) {
            for (int i = 0; i < xLen; i++) {
                newType[i][j] = type[yLen - 1 - j][i];
            }
        }

        return newType;
    }
}
````
