``` java
import java.util.*;

class Solution {
    public int solution(String[] lines) {
        PriorityQueue<Request> readyQueue = new PriorityQueue<>((r1, r2) -> {
            return r1.startTime - r2.startTime;
        });

        PriorityQueue<Request> processQueue = new PriorityQueue<>((r1, r2) -> {
            return r1.endTime - r2.endTime;
        });

        for (String log : lines) {
            String[] logArray = log.split(" ");

            int endTime = timeToMs(logArray[1]);
            int duration = secToMs(logArray[2].replaceAll("s$", ""));
            int beginTime = endTime - duration + 1;

            readyQueue.offer(new Request(beginTime, endTime));
        }

        int time = readyQueue.peek().startTime;
        int maxTask = Integer.MIN_VALUE;

        while (!readyQueue.isEmpty()) {
            while (!processQueue.isEmpty() && processQueue.peek().endTime < (time - 1000 + 1)) {
                processQueue.poll();
            }

            while (!readyQueue.isEmpty() && readyQueue.peek().startTime <= time) {
                processQueue.offer(readyQueue.poll());
            }

            maxTask = Math.max(maxTask, processQueue.size());

            if (!readyQueue.isEmpty()) {
                time = readyQueue.peek().startTime;
            }
        }

        return maxTask;
    }

    private int timeToMs(String stringTime) {
        String[] time = stringTime.split(":");
        int hour = Integer.parseInt(time[0]) * 3600 * 1000;
        int min = Integer.parseInt(time[1]) * 60 * 1000;
        int sec = (int) (Double.parseDouble(time[2]) * 1000);

        return hour + min + sec;
    }

    private int secToMs(String stringSec) {
        return (int) (Double.parseDouble(stringSec) * 1000);
    }
}

class Request {
    int startTime;
    int endTime;

    Request(int startTime, int endTime) {
        this.startTime = startTime;
        this.endTime = endTime;
    }
}
```
