#### 상황
- 물품의 금액 계산  
- 상황에 따라 물품의 금액이 달라짐  

#### 문제 코드
``` java
class Calculator {
    public int calculate(boolean firstGuest, List<Item> items) {
        int sum = 0;
        
        for (Item item : items) {
            if (firstGuest) {
                sum += (int) (item.getPrice() * 0.9);
            } else if (!item.isFresh()) {
                sum += (int) (item.getPrice() * 0.9);
            } else {
                sum += item.getPrice();
            }
        }
        
        return sum;
    }
}
```

- 위 구조에서는 물품 계산에 대한 새로운 정책이 매번 추가될 때마다 조건문이 새롭게 추가되어야 함  
- if 블록이 증가하게 되고 정책 종류에 따라 메소드가 매우 복잡해질 수 있음  


#### Strategy 패턴 적용 
``` java
public interface DiscountStrategy {
  int getDiscountPrice(item item);
}

public class FirstGuestDiscountStragety implements DiscountStrategy {
  int getDiscountPrice(item item) {
  
  }
}

public class LastGuestDiscountStragety implements DiscountStrategy {
  int getDiscountPrice(item item) {
  
  }
}

class Calculator {
    private DiscountStrategy discountStrategy;
    
    public Calculator(DiscountStrategy discountStrategy) {
        this.discountStrategy = discountStrategy;
    }
    
    public int calculate(List<Item> items) {
        int sum = 0;

        for (Item item : items) {
            sum += discountStrategy.getDiscountPrice(item);
        }

        return sum;
    }
}
```

- 정책별로 DiscountStrategy를 새로이 구현한고 이를 Calculator 클래스에서 정책에 맞게 변경하는 방식으로 구현한다면 훨씬 코드가 간결해진다  
