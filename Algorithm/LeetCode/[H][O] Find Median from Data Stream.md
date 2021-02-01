#### PriorityQueue - log n

``` java
class MedianFinder {
    PriorityQueue<Integer> lower;
    PriorityQueue<Integer> higher;    

    /** initialize your data structure here. */
    public MedianFinder() {
        lower = new PriorityQueue<>((a1, a2) -> {
            return a2 - a1;
        });
        higher = new PriorityQueue<>();
    }
    
    public void addNum(int num) {        
        lower.offer(num);
        higher.offer(lower.poll());
        
        if (higher.size() > lower.size()) {
            lower.offer(higher.poll());
        }
    }
    
    public double findMedian() {
        double median;
        
        if (lower.size() > higher.size()) {
            median = lower.peek();
        } else {
            median = ((double) higher.peek() + (double) lower.peek()) / (double) 2;
        }
        
        return median;
    }
}
```

#### ArrayList - O(nlogn)

``` java
class MedianFinder {
    ArrayList<Integer> list;

    /** initialize your data structure here. */
    public MedianFinder() {
        list = new ArrayList<>();
    }
    
    public void addNum(int num) {
        list.add(num);
    }
    
    public double findMedian() {
        double median = Double.MIN_VALUE;
        
        Collections.sort(list);
        
        int size = list.size();
        if (size % 2 == 1) {
            median = list.get(size / 2);
        } else {
            median = ((double) list.get(size / 2) + (double) list.get((size / 2) - 1)) / (double) 2;
        }
        
        return median;
    }
}
```
