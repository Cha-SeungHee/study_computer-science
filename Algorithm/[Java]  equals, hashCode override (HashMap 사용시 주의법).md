##### 
Java에서 HashMap 및 HashSet과 같은 자료구조에 기본형이 아닌 새로운 객체형 타입의 인스턴스를 저장할 때  
equals 및 hashCode 함수를 Override 하지 않으면 Hash가 의도한대로 동작하지 않는걸 알 수 있다  
- equals: 객체의 내용이 동일한지 비교하는 함수
- hashCode: 해당 클래스의 hashing시 사용되는 함수

#### hashCode와 관련된 일반 규약
- equals(Object)메소드가 true이면 두 객체의 hashCode 값은 같아야 한다  
- equals(Object)메소드가 false이면 두 객체의 hashCode가 꼭 다를 필요는 없다  
- 하지만 서로 다른 hashCode 값이 나오면 해시 테이블(hash table)의 성능이 향상될 수 있다는 점은 이해하고 있어야 한다.  

#### Override 하지 않았을 시
```java  
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException{
        HashMap<Node, Boolean> map = new HashMap<>();

        ArrayList<Node> list = new ArrayList<>();

        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(1);
        Node node5 = new Node(4);
        Node node6 = new Node(5);

        list.add(node1);
        list.add(node2);
        list.add(node3);
        list.add(node4);
        list.add(node5);
        list.add(node6);

        for (Node node : list) {
            if (map.containsKey(node)) {
                System.out.println("Duplicate");
            } else {
                System.out.println("New");
                map.put(node, true);
            }
        }
    }

    static class Node {
        int num;

        Node(int num) {
            this.num = num;
        }
    }
}
```

##### 출력결과물
New  
New  
New  
New  
New  
New  

1을 원소로 가지는 객체가 둘이 있으나 모두 새로운 객체로 인식됨을 알 수 있음  

```java  
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException{
        HashMap<Node, Boolean> map = new HashMap<>();

        ArrayList<Node> list = new ArrayList<>();

        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(1);
        Node node5 = new Node(4);
        Node node6 = new Node(5);

        list.add(node1);
        list.add(node2);
        list.add(node3);
        list.add(node4);
        list.add(node5);
        list.add(node6);

        for (Node node : list) {
            if (map.containsKey(node)) {
                System.out.println("Duplicate");
            } else {
                System.out.println("New");
                map.put(node, true);
            }
        }
    }

    static class Node {
        int num;

        Node(int num) {
            this.num = num;
        }

        @Override
        public boolean equals(Object obj) {
            return num == ((Node)obj).num;
        }

        @Override
        public int hashCode() {
            return num%10;
        }
    }
}

```

##### 출력결과물
New  
New  
New  
Duplicate  
New  
New  

1을 원소로 가지는 객체를 같은 객체로 인식  
