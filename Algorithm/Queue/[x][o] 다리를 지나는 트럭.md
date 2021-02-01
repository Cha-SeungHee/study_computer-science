```` java
import java.util.*;

class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int time = 0;
        int next = 0;
        int totalWeight = 0;

        Queue<Truck> queue = new LinkedList<>();

        while (next < truck_weights.length || !queue.isEmpty()) {
            int size = queue.size();

            /* 기존 트럭 이동 */
            for (int k = 0; k < size; k++) {
                Truck truck = queue.poll();
                truck.position = truck.position + 1;

                if (truck.position > bridge_length) {
                    totalWeight = totalWeight - truck.weight;
                } else {
                    queue.offer(truck);
                }
            }

            /* 신규 트럭 진입 */
            if (next < truck_weights.length && totalWeight + truck_weights[next] <= weight) {
                queue.offer(new Truck(1, truck_weights[next]));

                totalWeight = totalWeight + truck_weights[next];
                next = next + 1;
            }

            time = time + 1;
        }

        return time;
    }
}

class Truck {
    int position;
    int weight;

    Truck(int position, int weight) {
        this.position = position;
        this.weight = weight;
    }
}
````
