#### Visitor Pattern 
방문자와 방문 공간을 분리하여 방문 공간이 방문자를 맞이할 때, 이후에 대한 행동을 방문자에게 위임하는 패턴  

- 객체 스스로 객체가 하는 행동을 메소드로 가지고 있는 일반적인 OOP와 달리 행동의 대상이 되는 객체가 행동을 일으키는 객체를 입력으로 받음  
- "나는 상점에 방문한다. 나는 ~를 한다" -> "상점에 내가 방문을 했다. 내가 ~를 하게 한다"  
- '상점'이라는 객체가 '나'라는 객체를 입력 받은 후 '나'의 행동을 호출  
- '방문자'가 아니라 '방문 공간'의 입장에서 먼저 생각해보게 된다  

#### 구성요소
- Visitor  
- Element (Visitable)  
- ConcreteVisitor  
- ConcreteElement  

#### 장점 
- 작업 대상(방문 공간)과 작업 항목(방문 공간을 가지고 하는 일)을 분리  
- 작업 대상(방문 공간)은 단지 데이터를 담고있는 자료구조로 만들고, 작업 주체(방문자)는 visit() 안에 이 작업 대상을 입력받아 작업 항목을 처리  
- 즉, 데이터와 알고리즘이 분리되어, 데이터의 독립성을 높여준다.
- 작업 대상의 입장에서는 accept()로 인터페이스를 통일시켜, 사용자에게 동일한 인터페이스 제공  

#### 단점 
- 새로운 작업 대상(방문 공간)이 추가될 때마다 작업 주체(방문자)도 이에 대한 로직을 추가해야 한다  
- 두 객체 (방문자와 방문 공간)의 결합도가 높아진다  (서로 visit() 과 accept() 에 의존하므로)  

#### 활용  
- 자료 구조(데이터)와 자료 구조를 처리하는 로직(알고리즘)을 분리해야할 경우  
- 데이터 구조보다 알고리즘이 더 자주 바뀌는 경우  
- 즉, 방문공간은 어느정도 정해져있고 방문자가 더 자주 바뀌는 경우  


#### interface - Visitor
``` java
public interface Visitor {
    public void visit(Visitable visitable);
}
```

#### interface - Visitable
``` java
public interface Visitable {
    public void accept(Visitor visitor);
}
```

#### VisitorA
- Visitable의 데이터를 받아서 처리  

``` java
public class VisitorA implements Visitor {
    private int ageSum;

    public VisitorA() {
        ageSum = 0;
    }

    @Override
    public void visit(Visitable visitable) {
        if (visitable instanceof VisitableA) {
            ageSum += ((VisitableA) visitable).getAge();
        }
    }

    public int getAgeSum() {
        return ageSum;
    }
}
```

#### VisitableA
- 데이터 보관  
- accept: visitor의 visit 함수 호출  

``` java
public class VisitableA implements Visitable {
    private int age;

    public VisitableA(int age) {
        this.age = age;
    }

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

#### Main
``` java
import java.util.*;

class Main {
    public static void main(String[] args) {
        ArrayList<VisitableA> visitbales = new ArrayList<>();

        visitbales.add(new VisitableA(1));
        visitbales.add(new VisitableA(2));
        visitbales.add(new VisitableA(3));
        visitbales.add(new VisitableA(4));
        visitbales.add(new VisitableA(5));

        VisitorA visitor = new VisitorA();

        for (Visitable visitable : visitbales) {
            visitor.visit(visitable);
        }

        System.out.println(visitor.getAgeSum());
    }
}
```
