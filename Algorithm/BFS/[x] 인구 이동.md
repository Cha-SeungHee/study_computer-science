## BFS Visited 설정 시 주의할 점
- union: 일반적인 BFS Visited와 유사한 역할

#### 문제 코드 
- Parameter로 들어온 시작점 (y, x)에 대해 별도로 union, nodeList, queue 등 처리를 해주기 싫어서 offer 시점이 아닌 poll 이후에 일괄 처리  
- 문제 상황: 해당 Node가 Poll되기 전까지 다른 node를 통해 해당 위치가 접근되면 queue에 중복진입 가능하게 됨  

```` java
private static void bfs(int y, int x, int index) {
  int sum = 0, count = 0;
  ArrayList<Node> nodeList = new ArrayList<>();
  Queue<Node> queue = new LinkedList<>();

  queue.offer(new Node(y, x));
  while (!queue.isEmpty()) {
      Node node = queue.poll();

      union[node.y][node.x] = index;
      nodeList.add(node);
      sum = sum + board[node.y][node.x];
      count = count + 1;

      for (int k = 0; k < 4; k++) {
          int ny = node.y + dy[k];
          int nx = node.x + dx[k];

          if (0 <= nx && nx <= N - 1 && 0 <= ny && ny <= N - 1 && union[ny][nx] == -1) {
              int diff = Math.abs(board[ny][nx] - board[node.y][node.x]);

              if (L <= diff && diff <= R) {
                  queue.offer(new Node(ny, nx));
              }
          }
      }
  }
````

#### 정답 코드  
- offer 시점에 처리를 해주어 다른 노드를 통해 다시 접근되었을 때 중복 offer 불가  

```` java
private static void bfs(int y, int x, int index) {
    int sum = 0, count = 0;
    ArrayList<Node> nodeList = new ArrayList<>();
    Queue<Node> queue = new LinkedList<>();

    union[y][x] = index;
    nodeList.add(new Node(y, x));
    sum = sum + board[y][x];
    count = count + 1;

    queue.offer(new Node(y, x));
    while (!queue.isEmpty()) {
        Node node = queue.poll();

        for (int k = 0; k < 4; k++) {
            int ny = node.y + dy[k];
            int nx = node.x + dx[k];

            if (0 <= nx && nx <= N - 1 && 0 <= ny && ny <= N - 1 && union[ny][nx] == -1) {
                int diff = Math.abs(board[ny][nx] - board[node.y][node.x]);

                if (L <= diff && diff <= R) {
                    union[ny][nx] = index;
                    nodeList.add(new Node(ny, nx));
                    sum = sum + board[ny][nx];
                    count = count + 1;

                    queue.offer(new Node(ny, nx));
                }
            }
        }
    }

    for (Node n : nodeList) {
        board[n.y][n.x] = sum / count;
    }
}
````

#### 정답 코드 (전체)
``` java
import java.util.*;
import java.io.*;

class Main {
    static int N, L, R;

    static int[][] board;
    static int[][] union;

    static int[] dx = {1, 0, -1, 0}; // right, up, left, down
    static int[] dy = {0, -1, 0, 1};

    public static void main(String[] args) throws IOException {
        int count = 0;
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());

        board = new int[N][N];
        union = new int[N][N];

        for (int j = 0; j < N; j++) {
            st = new StringTokenizer(br.readLine(), " ");

            for (int i = 0; i < N; i++) {
                board[j][i] = Integer.parseInt(st.nextToken());
            }
        }

        while (true) {
            int index = 0;

            for (int j = 0; j < N; j++) {
                for (int i = 0; i < N; i++) {
                    union[j][i] = -1;
                }
            }

            for (int j = 0; j < N; j++) {
                for (int i = 0; i < N; i++) {
                    if (union[j][i] == -1) {
                        bfs(j, i, index);
                        index = index + 1;
                    }
                }
            }

            if (index == N * N) break;

            count = count + 1;
        }

        bw.write(count + "\n");
        bw.flush();
    }

    private static void bfs(int y, int x, int index) {
        int sum = 0, count = 0;
        ArrayList<Node> nodeList = new ArrayList<>();
        Queue<Node> queue = new LinkedList<>();

        union[y][x] = index;
        nodeList.add(new Node(y, x));
        sum = sum + board[y][x];
        count = count + 1;

        queue.offer(new Node(y, x));
        while (!queue.isEmpty()) {
            Node node = queue.poll();

            for (int k = 0; k < 4; k++) {
                int ny = node.y + dy[k];
                int nx = node.x + dx[k];

                if (0 <= nx && nx <= N - 1 && 0 <= ny && ny <= N - 1 && union[ny][nx] == -1) {
                    int diff = Math.abs(board[ny][nx] - board[node.y][node.x]);

                    if (L <= diff && diff <= R) {
                        union[ny][nx] = index;
                        nodeList.add(new Node(ny, nx));
                        sum = sum + board[ny][nx];
                        count = count + 1;

                        queue.offer(new Node(ny, nx));
                    }
                }
            }
        }

        for (Node n : nodeList) {
            board[n.y][n.x] = sum / count;
        }
    }

    static class Node {
        int y, x;

        Node (int y, int x) {
            this.y = y;
            this.x = x;
        }
    }
}
```
