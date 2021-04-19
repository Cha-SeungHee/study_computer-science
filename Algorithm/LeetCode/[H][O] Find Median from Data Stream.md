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

``` py
import heapq


class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.lower_heap = []
        self.higher_heap = []
        

    def addNum(self, num: int) -> None:
        heapq.heappush(self.lower_heap, -num)
        heapq.heappush(self.higher_heap, -heapq.heappop(self.lower_heap))
        
        if len(self.higher_heap) > len(self.lower_heap):
            heapq.heappush(self.lower_heap, -heapq.heappop(self.higher_heap))

    def findMedian(self) -> float:
        if not self.lower_heap:
            return None        
        elif len(self.lower_heap) == len(self.higher_heap):
            return (-self.lower_heap[0] + self.higher_heap[0]) / 2
        else:
            return -self.lower_heap[0]
        
        


# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```
