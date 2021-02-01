```java 
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0) return null;
        
        ArrayList<ListNode> list = new ArrayList<>();
        for (ListNode node : lists) {
            list.add(node);
        }        
        
        while (list.size() > 1) {
            ArrayList<ListNode> tmpList = new ArrayList<>();
            int size = list.size();
            
            for (int i=0; i<size; i=i+2) {
                ListNode node1 = list.get(i);
                ListNode node2 = null;
                if (i+1 < size) node2 = list.get(i+1) ;                
                
                ListNode node = merge(node1, node2);
                tmpList.add(node);
            }
            
            list = tmpList;
        }
        
        return list.get(0);
    }
    
    private ListNode merge(ListNode node1, ListNode node2) {
        if (node1 == null && node2 == null) return null;
        if (node1 == null) return node2;
        if (node2 == null) return node1;
        
        ListNode head = null;
        ListNode cur = null;
        
        while (node1 != null && node2 != null) {
            if (node1.val <= node2.val) {
                if (head == null) {
                    head = node1;
                    cur = node1;
                    node1 = node1.next;
                } else {
                    cur.next = node1;
                    cur = cur.next;
                    node1 = node1.next;
                }
            } else {
                if (head == null) {
                    head = node2;
                    cur = node2;
                    node2 = node2.next;
                } else {
                    cur.next = node2;
                    cur = cur.next;
                    node2 = node2.next;
                }
            }
        }
        
        while (node1 != null) {
            cur.next = node1;
            node1 = node1.next;
            cur = cur.next;
        }
        
        while (node2 != null) {
            cur.next = node2;
            node2 = node2.next;
            cur = cur.next;
        }        
        
        return head;
    }
}
``` 

```java 
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0) return null;
        
        ListNode head = null;
        ListNode cur = null;
        
        Queue<ListNode> pq = new PriorityQueue<>((n1,n2)->n1.val-n2.val);
        for (ListNode node : lists) {
            ListNode tmp = node;
            ListNode prev = null;
            while (tmp != null) {
                prev = tmp;
                pq.offer(tmp);
                tmp = tmp.next;
                prev.next = null;
            }
        }
        
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            if (head == null) {
                head = node;
                cur = node;
            } else {
                cur.next = node;
                cur = cur.next;
            }
        }
            
        return head;
    }
}
```java 

#### 확인
1. 람다식 확인
2. PriorityQueue : 람다식에 따라서 정렬순서 달라지는 부분 확인
