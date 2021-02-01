PriorityQueue의 정렬순서는 일반 Sort의 정렬순서와 동일

```java  

public static void main(String[] args) throws IOException{
    ArrayList<Item> list = new ArrayList<>();
    PriorityQueue<Item> pq = new PriorityQueue<>();

    for (int i=0; i<5; i++) {
        Item item = new Item(i);
        list.add(item);
        pq.offer(item);
    }

    Collections.sort(list);

    for (int i=0; i<5; i++) {
        System.out.println(list.get(i).num); // 출력결과: 0 1 2 3 4
        System.out.println(pq.poll().num); // 출력결과: 0 1 2 3 4
        System.out.println();
    }
}    

static class Item implements Comparable<Item> {
    int num;

    Item (int num) {
        this.num = num;
    }


    @Override
    public int compareTo(Item o) {
        return (num > o.num) ? 1 : -1;
    }
}
```
