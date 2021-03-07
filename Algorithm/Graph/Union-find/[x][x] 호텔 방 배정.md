``` java
import java.util.*;

class Solution {
    public long[] solution(long k, long[] room_number) {
        long[] answer = new long[room_number.length];
        HashMap<Long, Long> map = new HashMap<>();

        for (int i = 0; i < room_number.length; i++) {
            answer[i] = getNextRoom(map, room_number[i]);
        }

        return answer;
    }

    private long getNextRoom(HashMap<Long, Long> map, long room) {
        if (!map.containsKey(room)) {
            map.put(room, room + 1);
            return room;
        }

        map.put(room, getNextRoom(map, map.get(room)));

        return map.get(room);
    }
}
```
