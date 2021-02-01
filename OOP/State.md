#### 상황
- 자판기  

#### 문제 코드
``` java
class VendingMachine {
    public static enum State {NOCOIN, SELECTABLE}
    
    private State state = State.NOCOIN;
    
    public void insertCoint(int coin) {
        switch(state) {
            case NOCOIN:
                increaseCoin(coin);
                state = State.SELECTABLE;
                break;
                
            case SELECTABLE:
                increaseCoin(coin);
                break;
        }
    }
    
    public void select(int productId) {
        switch(state) {
            case NOCOIN:
                /* do nothing */
                break;

            case SELECTABLE:
                provideProduct(productId);
                decreaseCoin();
                if (hasNoCoin()) {
                    state = State.NOCOIN;
                }
                
                break;
        }
    }    
}
```

- 새로운 State를 추가하거나 뺄 때마다 insertCoin과 select() 메소드에 동일하게 새로운 조건문이 추가되어야 한다  

#### State 패턴 적용
``` java
interface State {
    void increaseCoin(int coin);

    void select(int productId);
}

class NoCoinState implements State {

    @Override
    public void increaseCoin(int coin) {

    }

    @Override
    public void select(int productId) {

    }
}

class SelectableState implements State {

    @Override
    public void increaseCoin(int coin) {

    }

    @Override
    public void select(int productId) {

    }
}

class VendingMachine {
    private State state;

    public VendingMachine() {
        state = new NoCoinState();
    }

    public void insertCoint(int coin) {
        state.increaseCoin(coin);
    }

    public void select(int productId) {
        state.select(productId);
    }
}
```

- State 객체를 만들어 insertCoin, select 메소드를 구현  
- Vending machine 코드 훨씬 단순화  

#### State의 변경 주체
- 콘텍스트 객체 또는 상태 객체에서 할 지는 프로그램의 특성에 따라 판단  

#### vs Strategy 패턴
- Strategy 패턴과 유사  
- Strategy 패턴: 동일한 틀 안에 있는 특정 작업 장식 모드를 바꿔줄 때  
- State 패턴: 상태에 따라 다르게 할 일과 함께 모듈화해서 지정  
