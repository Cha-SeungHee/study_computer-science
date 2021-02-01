```` java
import java.util.*;

class Main {
    public static void main(String[] args) {
        int result = 0;


        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (int i = 0; i < N; i++) {
            pq.offer(sc.nextInt());
        }

        while (pq.size() != 1) {
            int one = pq.poll();
            int two = pq.poll();

            int sum = one + two;

            result = result + sum;

            pq.offer(sum);
        }

        System.out.println(result);
    }
}
````

#### 확인
1. pq.size() == 1인 경우: 이미 한 묶음이 되어 비교할 필요가 없는 경우   
2. 매번 최소 묶음과 계산하기 위해서 합친 묶음 또한 pq에 넣어줘야 한다  
