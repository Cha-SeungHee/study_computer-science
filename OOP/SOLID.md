## SOLID

- S (Single Responsibility)  
- O (Open-closed)  
- L (Liskov substitution)  
- I (Interface segregation)  
- D (Dependency Inversion)  



## 1. S (Single Responsibility)
- 클래스는 단 한 개의 책임을 가져야 한다 
- 클래스가 여러 책임을 갖게 되면 각 책임마다 변경되는 이유가 발생하기 때문 

예시) DataViewer 클래스 (위반)
- 데이터 읽는 책임 
- 화면에 보여주는 책임  

``` java
class DataViewer {

    public void display() {
        String data = loadHtml();
        updateGui(data);
    }

    public String loadHtml() {
        HttpClient client = new HttpClient();
        client.connect(url);
        return client.getResponse();
    }

    private void updateGui(String data) {
        GuiData guiModel = parseDataToGuiData(data);
        tableUI.changeData(guiModel);
    }

    private GuiData parseDataToGuiData(String data) {
        //
    }
}
```

문제상황  
- 서버가 HTTP 프로토콜에서 소켓 기반의 프로토콜로 변경되면 (응답 데이터 형식 변경) loadHtml() 
메소드 이외에 display(), updateGui, parseDataToGuiData 메소드 등도 변경되어야 한다  


## 2. O (Open-closed principle)
- 확장에는 열려 있어야 하고, 변경에는 닫혀 있어야 한다  
- 기능을 변경하거나 확장할 수 있으면서 그 기능을 사용하는 코드는 수정하지 않는다  
- 변화가 예상되는 것을 추상화해서 변경의 유연함을 얻도록 해준다  


주요 방법
1) 인터페이스
- 기능을 사용하는 코드는 인터페이스의 메소드를 호출
- 새로운 기능을 추가하여야 할 때는 해당 인터페이스를 구현

2) 상속
- 기능을 사용하는 코드는 상위 클래스의 메소드를 호출
- 새로운 기능 추가시 상위 클래스를 확장하는 하위 클래스 구현


## 3. L (Liskov substitution principle)
- 상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다 
- 개념적으로 상속 관계에 있는 클래스들을 실제로 구현할 때는 상속 관계가 아닐 수도 있음을 염두해야 한다
- 부모 클래스와 하위 클래스의 동작성이 일관되어야 개방 폐쇄 법칙에서처럼 인터페이스 또는 상위 클래스의 메소드를 호출했을 때 문제가 발생하지 않는다
- 리스코프 치환 원칙이 제대로 지켜지지 않으면 다형성에 기반한 개방 폐쇄 원칙 역시 지켜지지 않는다


## 4. I (Interface segregation principle)
- A가 B에 의존할 경우 B의 변화로 인해 A가 변경되기도 하지만 A의 요구에 의해 B가 변경되기도 한다  
- 즉, 인터페이스를 분리하는 기준이 인터페이스를 사용하는 클라이언트가 되어야 한다  
- 각 클라이언트가 사용하는 기능을 중심으로 인터페이스를 분리함으로써 클라이언트로부터 발생하는 인터페이스 
변경의 여파가 다른 클라이언트에 미치는 영향을 최소화  


## 5. D (Dependency inversion principle)
- 고수준 모듈은 저수준 모듈의 구현에 의존해서는 안된다  
- 저수준 모듈이 고수준 모듈에서 정의한 추상 타입에 의존해야 한다  

- 고수준 모듈 : 단일 기능을 제공하는 모듈 (바이트 데이터를 읽어와 암호화하고 결과 사용)  
- 저수준 모듈 : 고수준 모듈의 기능을 구현하기 위해 필요한 하위 기능을 실제 구현으로 정의 (파일에서 바이트 데이터 읽기. AES 알고리즘으로 암호화. 파일에 바이트 데이터 사용)  
- 저수준 모듈이 고수준 모듈을 의존한다 -> 추상화  
- 리스코프 치환 원칙과 개방 폐쇄 원칙을 따르는 설계를 만들어주는 기반



